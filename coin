import requests
from bs4 import BeautifulSoup
import csv

def get_coinmarket_data():
    url = "https://coinmarketcap.com"
    response = requests.get(url)
    if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
        # Находим все строки таблицы с криптовалютами
        table_rows = soup.find_all('tr')

        # Создаем файл для записи данных
        with open('crypto_data.csv', 'w', newline='', encoding='utf-8') as csvfile:
            writer = csv.writer(csvfile)
            # Записываем заголовки столбцов
            writer.writerow(['Название', 'Цена', 'Рост за 7 дней', 'Рыночная капитализация'])

            for row in table_rows[1:]:  # Пропускаем первую строку с заголовками
                # Получаем данные из ячеек таблицы
                cells = row.find_all('td')
                if len(cells) >= 10:
                    name = cells[2].text.strip()
                    price = cells[3].text.strip()
                    change_7d = cells[6].text.strip()
                    market_cap = cells[7].text.strip()

                    # Проверяем, что рост за 7 дней указан и больше 0
                    if change_7d and change_7d != '?' and float(change_7d[:-1]) > 0:
                        # Записываем данные в файл
                        writer.writerow([name, price, change_7d, market_cap])

        print("Данные успешно записаны в файл crypto_data.csv")

if __name__ == "__main__":
    get_coinmarket_data()
