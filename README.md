# MZNovels

> **This repository is private.** MZNovels is a live production application
> with real user accounts, published content, and credentials that can't be
> safely open-sourced. Exposing the codebase would put real users at risk —
> so this public repo exists purely to verify the project for recruiters and
> collaborators.
>
> The full technical case study — architecture decisions, deployment
> challenges, traffic analysis, and verification documents — is here:
>
> **[zaouk.dev/case-study/mznovels →](https://zaouk.dev/case-study/mznovels)**
>
> I'm happy to walk through the code directly in an interview.

---

A completely free novel reading and publishing platform, built and operated solo for over two years.
Writers can publish their work, and readers can discover and read freely — no subscriptions, no paywalls.
Serving over **100,000 genuine users** and **4M+ page views** with no marketing budget.

## Highlights

- Built and deployed solo from scratch — backend, frontend, infrastructure, and ops
- Custom OAuth2 authentication backend (Google sign-in) alongside Django's native auth system
- Full-text search across novels and chapters powered by Whoosh (no external search service)
- Dockerized deployment on a Linux VPS with Nginx, Gunicorn, and MySQL
- Diagnosed and mitigated a sustained bot traffic campaign using container-level log analysis and Nginx rate limiting

## Features

### For Readers
- Browse and read novels for free — no subscription or paywall
- Advanced search and filtering by genre, tags, and ranking
- Bookmark novels and track reading progress across chapters
- User profiles with avatars
- Sign in with Google via OAuth2

### For Writers
- Publish and manage novels from a dedicated writer dashboard
- Full chapter editor with rich-text formatting
- Chapter ordering and management tools
- Cover image uploads and novel metadata editing

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Django, Python |
| Frontend | HTML5, CSS3, JavaScript |
| Database | MySQL |
| Search | Whoosh |
| Auth | Django Auth + Custom OAuth2 (Google) |
| Infrastructure | Docker, Nginx, Gunicorn, VPS (Linux / Vultr) |

## Architecture Overview

The application is a Django monolith — the right call for a solo project where shipping speed and Django's mature ecosystem (admin panel, ORM, built-in auth) mattered more than distributed services. The frontend is server-rendered with Django templates; no separate SPA layer, which kept the deployment surface manageable.

The stack runs across four Docker containers:

- **Web** — Django application served via Gunicorn
- **Nginx** — reverse proxy, static file serving, SSL termination, and rate limiting
- **Database** — MySQL, with a dedicated initialization container for setup and migrations

Authentication is handled by a custom OAuth2 backend (`oauth2_backend.py`, `adapters.py`, `backends.py`) layered on top of Django's auth system, so user sessions stay entirely under application control with no third-party auth dependency.

For the full write-up on challenges, bot traffic mitigation, and lessons learned, see the [case study](https://zaouk.dev/case-study/mznovels).

## Project Structure

```
MZNovels-website/
├── nginx/                  # Reverse proxy config
├── mysql-init/             # DB initialization scripts
├── myapp/                  # Django application
│   ├── management/         # Custom management commands
│   ├── migrations/         # Database schema history
│   ├── static/             # App-level static assets
│   ├── templates/          # HTML templates
│   ├── templatetags/       # Custom template tags
│   ├── tests/              # Test suite
│   ├── adapters.py         # OAuth2 adapter
│   ├── backends.py         # Auth backends
│   ├── middleware.py       # Access control
│   ├── models.py
│   ├── oauth2_backend.py   # Custom OAuth2 backend
│   ├── scraper.py          # Content ingestion
│   ├── search_indexes.py   # Whoosh search config
│   ├── sitemaps.py         # SEO sitemap generation
│   ├── urls.py
│   ├── validators.py
│   └── views.py
├── Novelwebsite/           # Project configuration
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── staticfiles/
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
└── manage.py
```

## Verification

Ownership and traffic analytics are documented in the [case study](https://zaouk.dev/case-study/mznovels), including a domain purchase receipt and Google Analytics exports.

## License

Free to use and read. All rights reserved for published content belong to their respective authors.
