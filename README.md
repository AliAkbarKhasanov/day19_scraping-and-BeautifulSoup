# День 19 — Парсинг сайтов (requests, BeautifulSoup)

**Цель:** Научиться автоматически получать данные с веб-страниц и извлекать нужную информацию (цитаты и авторов).

## Что внутри
- `day19_scraping_quotes.py` — скрипт, который парсит https://quotes.toscrape.com/ по всем страницам и сохраняет **цитаты — авторы** в `outputs/quotes.txt`.
- `requirements.txt` — зависимости проекта.
- `outputs/quotes.txt` — результат работы скрипта (игнорируется в гите через `.gitignore`).

## Установка и запуск
```bash
# 1) Клонируем проект (или перейдите в папку проекта)
git clone <ваш-URL-репозитория>
cd path-to-million/day19_scraping

# 2) (рекомендуется) создаём и активируем виртуальное окружение
python -m venv .venv
# Windows:
.venv\\Scripts\\activate
# macOS/Linux:
source .venv/bin/activate

# 3) Ставим зависимости
pip install -r requirements.txt

# 4) Запуск
python day19_scraping_quotes.py
