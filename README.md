# MZNovels

A completely free novel platform built for both writers and readers.
Writers can publish their work, and readers can discover and read freely — no subscriptions, no paywalls.

## Features

### For Readers
- Browse and read novels for free
- Advanced search and filtering by genre, tags, and ranking
- Bookmark and track reading progress
- User profiles and avatars

### For Writers
- Publish and manage novels
- Full writing editor
- Chapter management

## Tech Stack

- **Backend** — Django + Python
- **Frontend** — HTML, CSS, JavaScript
- **Search** — Whoosh
- **Server** — Nginx/Guinorne
- **Container** — Docker
- **DB** — MYSQL

## Getting Started

### Requirements
- Docker
- Python 3.x

### Run locally
```bash
git clone https://github.com/Mohammed-Zaouk/MZNovels-website.git
cd MZNovels-website
docker-compose up --build
```

### Without Docker
```bash
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

## License

Free to use and read. All rights reserved for published content belong to their respective authors.
