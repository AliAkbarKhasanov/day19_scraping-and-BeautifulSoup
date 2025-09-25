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

import requests  # получаем HTML-страницы
from bs4 import BeautifulSoup  # разбираем HTML

# Стартовый адрес (первая страница с цитатами)
url = "https://quotes.toscrape.com/"
page = 1  # счётчик страниц

# Откроем файл для сохранения результатов
# "w" — запись с перезаписью, UTF-8 — чтобы поддерживать любые символы
with open("outputs/quotes.txt", "w", encoding="utf-8") as f:
    while True:
        print(f"Парсим страницу {page}...")

        # Загружаем HTML текущей страницы
        response = requests.get(url)
        response.raise_for_status()  # бросит ошибку, если статус не 200

        # Разбираем HTML с помощью BeautifulSoup
        soup = BeautifulSoup(response.text, "html.parser")

        # Ищем все цитаты и соответствующих авторов
        quotes = soup.find_all("span", class_="text")
        authors = soup.find_all("small", class_="author")

        # Итерируемся по парам (цитата — автор)
        for q, a in zip(quotes, authors):
            line = f"{q.text} — {a.text}"
            print(line)
            f.write(line + "\n")

        # Ищем кнопку "Next" для перехода на следующую страницу
        next_btn = soup.find("li", class_="next")
        if next_btn:
            next_link = next_btn.find("a")["href"]
            url = "https://quotes.toscrape.com" + next_link
            page += 1
        else:
            break

print("✅ Все цитаты сохранены в файл outputs/quotes.txt")
