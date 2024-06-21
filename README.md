# Проект HeadHunter Data Collector

Этот проект предназначен для сбора данных с API HeadHunter (hh.ru) о работодателях и вакансиях, их сохранения в базу данных PostgreSQL и предоставления возможности работы с этими данными.

## Как запустить проект

1. **Настройка базы данных**:
   - Убедитесь, что у вас установлен и запущен PostgreSQL.
   - Создайте базу данных под названием `skypro`.
   - Запустите скрипт `db_settings.py` для создания необходимых таблиц. При необходимости измените параметры подключения (`dbname`, `user`, `password`, `host`, `port`).

2. **Сбор и вставка данных**:
   - Запустите скрипт `hh_data_collector.py` для получения данных о работодателях и вакансиях с API HeadHunter.
   - Убедитесь, что база данных PostgreSQL (`skypro`) доступна и работает.

3. **Операции с базой данных**:
   - Используйте `db_manager.py` для выполнения запросов к базе данных.
   - При необходимости измените параметры подключения (`dbname`, `user`, `password`, `host`, `port`).

## Функциональность

- **Сбор данных**:
  - `hh_data_collector.py`: Получает данные о работодателях и вакансиях с API HeadHunter и вставляет их в базу данных PostgreSQL (`skypro`).

- **Управление базой данных**:
  - `db_manager.py`: Предоставляет несколько методов для взаимодействия с базой данных:
    - `get_companies_and_vacancies_count()`: Возвращает количество вакансий, сгруппированных по работодателям.
    - `get_all_vacancies()`: Возвращает все вакансии с информацией о работодателе.
    - `get_avg_salary()`: Вычисляет среднюю зарплату вакансий.
    - `get_vacancies_with_higher_salary()`: Возвращает вакансии с зарплатой выше средней.
    - `get_vacancies_with_keyword(keyword)`: Возвращает вакансии, содержащие определенное ключевое слово.

## Пример использования

```python
# Пример использования db_manager.py
from db_manager import DBManager

db = DBManager(dbname='skypro', user='postgres', password='skypro', host='localhost', port='5433')

print("Количество компаний и вакансий:")
print(db.get_companies_and_vacancies_count())

print("\nВсе вакансии:")
print(db.get_all_vacancies())

print("\nСредняя зарплата:")
print(db.get_avg_salary())

print("\nВакансии с высокой зарплатой:")
print(db.get_vacancies_with_higher_salary())

print("\nВакансии с ключевым словом 'Python':")
print(db.get_vacancies_with_keyword('Python'))

db.close()
