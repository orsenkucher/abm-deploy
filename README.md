# Clone this repository

```bash
git clone https://github.com/orsenkucher/abm-deploy.git
cd abm-deploy
```

# Before you begin

- Установлен docker:
  - `docker version` что-то пишет
  - Доступна подпрограмма `docker compose`.
- Есть строка для подключения к PostgreSQL базе.
- Получен файлик `key.json` для подключения к приватному репозиторию.
- Заполнен `.env` файл

# Setup

## Устанавливаем `gcloud`

Это sdk от Google для авторизации и работы с их сервисами на GCP.
Пример для Debian:

```
sudo apt-get install apt-transport-https ca-certificates gnupg

echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

sudo apt-get update && sudo apt-get install google-cloud-sdk

```

После чего `gcloud` установлен и его нужно инициализировать

> Когда напишет что нужно войти в аккаунт - говорим нет

```
gcloud init # Say No for login prompt
```

## Используем `key.json` для получения прав на чтение контейнера из репозитория.

Активируем ключ в `gcloud`

```
gcloud auth activate-service-account --key-file <path to key file>
```

тут `<path to key file>` указывает на `key.json`

## Подключаем `gcloud` к докеру

Теперь докер начнет использовать `gcloud` для авторизации

```
gcloud auth configure-docker \
	us-central1-docker.pkg.dev
```

# Run

```
docker compose up
```
