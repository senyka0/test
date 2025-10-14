# 🚀 FastAPI Додаток для Декодування Приватних Ключів та Запуску Активностей

## 📌 Встановлення та Запуск
**Для запуску додатку вам необхідно Python 3.12.6** 

### 🔹 1. Створення та активація віртуального середовища
```sh
python -m venv venv
source venv/bin/activate  # для macOS та Linux
venv\Scripts\activate    # для Windows

```

### 🔹 2. Встановлення залежностей
```sh
pip install -r requirements.txt
```

### 🔹 3. Налаштування середовища (Для платної версії)
Створіть файл `.env` в кореневій директорії та додайте в нього:
```ini
LICENSE_KEY=ваш_токен_лицензии
```

### 🔹 4. Запуск додатку
```sh
uvicorn backend.api:app --host 0.0.0.0 --port 8000
```

### 🔹 Увага
**Якщо після запуску у вас буде помилка, пов'язана з «pyarmor_runtime.so»** \
**в такому випадку вам необхідно позначити файл як безпечний у налаштуваннях конфіденційності**

---

## 🌍 Основні ендпоінти

### 🔑 1. Декодування приватних ключів

✅ Оновіть файл `private_keys.txt`
✅ Додайте в нього приватні ключі ✅
Викличте ендпоінт:

```http
GET /v1/encode/accounts
```
Просто натисніть `Execute`, і приватні ключі будуть декодовані.

---

### 📝 2. Зміна accounts.csv
Файл `accounts.csv` має містити дані у наступному форматі:
```csv
id,name,address,private_key,proxy_url,seed_phrases,tags,additional_data
1,Dave,account_address,encoded_private_key,username:password@ip:port,,TEST_TAG,{}
```

---

### ⚙️ 3. Запуск активностей
📌 Для запуску пресету надішліть JSON на ендпоінт:
```http
POST /v1/start_preset/{csv}/
```
📌 У тілі запиту передайте:
```json
{
  "tags": ["TEST"],
  "project": "test_project",
  "module": "test_module",
  "settings": {
    "delay_retry_seconds": 0,
    "delay_between_activities": [0, 1],
    "max_retry_after_fail_txn": 0,
    "queue_threads_amount": 1,
    "proxy_type": "string",
    "network": "sepolia",
    "amount_boundaries": [0.8, 0.9],
    "found_balance": false,
    "min_amount": 0.2,
    "random_network": false,
    "task_count": 1
  }
}
```
🔹 Вкажіть restart=true, якщо хочете перезапустити зламані акаунти.

📌 Детальні пресети будуть надані в окремій документації під кожен проект.



---

### 📋 4. Перевірка всіх акаунтів
📌 Ендпоінт для перевірки всіх акаунтів:
```http
GET /v1/all_accounts/{csv}/
```
📌 Потрібно вказати тип файлу (`csv`), потім натиснути `Execute`.

---

### ❗ 5. Обробка помилок
🔹 Якщо під час виконання виникнуть помилки, вони будуть записані у CSV-файл з помилковими акаунтами.
🔹 Для їх повторної обробки потрібно надіслати запит на ендпоінт з параметром restart=true.


---

🔥 Тепер усе готово до роботи! Успішного використання! 🚀
