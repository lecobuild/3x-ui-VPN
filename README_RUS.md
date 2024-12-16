# 3X-UI

**Продвинутый веб-панель • Основан на Xray Core**

[![](https://img.shields.io/github/v/release/mhsanaei/3x-ui.svg)](https://github.com/MHSanaei/3x-ui/releases)
[![](https://img.shields.io/github/actions/workflow/status/mhsanaei/3x-ui/release.yml.svg)](#)
[![GO Version](https://img.shields.io/github/go-mod/go-version/mhsanaei/3x-ui.svg)](#)
[![Downloads](https://img.shields.io/github/downloads/mhsanaei/3x-ui/total.svg)](#)
[![License](https://img.shields.io/badge/license-GPL%20V3-blue.svg?longCache=true)](https://www.gnu.org/licenses/gpl-3.0.en.html)

> **Отказ от ответственности:** Данный проект предназначен исключительно для личного обучения и коммуникаций. Не используйте его в незаконных целях и в производственной среде.

**Если этот проект вам полезен, вы можете поставить**:star2:

<a href="#">
  <img width="125" alt="image" src="https://github.com/MHSanaei/3x-ui/assets/115543613/7aa895dd-048a-42e7-989b-afd41a74e2e1.jpg"></a>

- USDT (TRC20): `TXncxkvhkDWGts487Pjqq1qT9JmwRUz8CC`

## Установка и Обновление

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

## Установка пользовательской версии

Чтобы установить нужную вам версию, добавьте её к команде установки. Например, для версии `v2.1.3`:

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh) v2.1.3
```

## SSL Сертификат

<details>
  <summary>Нажмите для получения информации о SSL-сертификате</summary>

### Cloudflare

Скрипт управления имеет встроенное получение SSL-сертификата для Cloudflare. Для использования необходимо:

- Электронная почта, зарегистрированная в Cloudflare
- Глобальный API ключ Cloudflare
- Доменное имя, которое уже направлено через Cloudflare на текущий сервер

**1:** Выполните команду `x-ui` в терминале, затем выберите `Cloudflare SSL Certificate`.

### Certbot
```
apt-get install certbot -y
certbot certonly --standalone --agree-tos --register-unsafely-without-email -d вашдомен.com
certbot renew --dry-run
```

***Подсказка:*** *Certbot также встроен в скрипт управления. Вы можете выполнить команду `x-ui`, затем выбрать `SSL Certificate Management`.*
</details>

## Ручная установка и обновление

<details>
  <summary>Нажмите для деталей ручной установки</summary>

#### Использование

1. Чтобы загрузить последнюю версию архива непосредственно на сервер, выполните:

```sh
ARCH=$(uname -m)
case "${ARCH}" in
  x86_64 | x64 | amd64) XUI_ARCH="amd64" ;;
  i*86 | x86) XUI_ARCH="386" ;;
  armv8* | armv8 | arm64 | aarch64) XUI_ARCH="arm64" ;;
  armv7* | armv7) XUI_ARCH="armv7" ;;
  armv6* | armv6) XUI_ARCH="armv6" ;;
  armv5* | armv5) XUI_ARCH="armv5" ;;
  *) XUI_ARCH="amd64" ;;
esac

wget https://github.com/MHSanaei/3x-ui/releases/latest/download/x-ui-linux-${XUI_ARCH}.tar.gz
```

2. После загрузки выполните следующие команды для установки или обновления x-ui:

```sh
ARCH=$(uname -m)
case "${ARCH}" in
  x86_64 | x64 | amd64) XUI_ARCH="amd64" ;;
  i*86 | x86) XUI_ARCH="386" ;;
  armv8* | armv8 | arm64 | aarch64) XUI_ARCH="arm64" ;;
  armv7* | armv7) XUI_ARCH="armv7" ;;
  armv6* | armv6) XUI_ARCH="armv6" ;;
  armv5* | armv5) XUI_ARCH="armv5" ;;
  *) XUI_ARCH="amd64" ;;
esac

cd /root/
rm -rf x-ui/ /usr/local/x-ui/ /usr/bin/x-ui
tar zxvf x-ui-linux-${XUI_ARCH}.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

</details>

## Установка в Docker

<details>
  <summary>Нажмите для деталей о Docker</summary>

#### Использование

1. Установите Docker:

   ```sh
   bash <(curl -sSL https://get.docker.com)
   ```

2. Клонируйте репозиторий проекта:

   ```sh
   git clone https://github.com/MHSanaei/3x-ui.git
   cd 3x-ui
   ```

3. Запустите сервис

   ```sh
   docker compose up -d
   ```

   ИЛИ

   ```sh
   docker run -itd \
      -e XRAY_VMESS_AEAD_FORCED=false \
      -v $PWD/db/:/etc/x-ui/ \
      -v $PWD/cert/:/root/cert/ \
      --network=host \
      --restart=unless-stopped \
      --name 3x-ui \
      ghcr.io/mhsanaei/3x-ui:latest
   ```

Обновление до последней версии:

   ```sh
    cd 3x-ui
    docker compose down
    docker compose pull 3x-ui
    docker compose up -d
   ```

Удаление 3x-ui из docker:

   ```sh
    docker stop 3x-ui
    docker rm 3x-ui
    cd --
    rm -r 3x-ui
   ```

</details>

## Рекомендуемые ОС

- Ubuntu 20.04+
- Debian 11+
- CentOS 8+
- Fedora 36+
- Arch Linux
- Manjaro
- Armbian
- AlmaLinux 9+
- Rockylinux 9+

## Поддерживаемые архитектуры и устройства

<details>
  <summary>Нажмите для деталей о поддерживаемых архитектурах и устройствах</summary>

Наша платформа поддерживает широкий спектр архитектур и устройств, гарантируя гибкость в различных вычислительных средах:

- **amd64**: Распространённая архитектура для ПК и серверов.
- **x86 / i386**: Широко используется на настольных ПК и ноутбуках.
- **armv8 / arm64 / aarch64**: Оптимизирована для современных мобильных и встраиваемых устройств (Raspberry Pi 4, 3, Zero 2 и т.д.).
- **armv7 / arm / arm32**: Для более старых мобильных и встраиваемых устройств (Orange Pi Zero LTS, Raspberry Pi 2 и др.).
- **armv6 / arm / arm32**: Для очень старых встраиваемых устройств (Raspberry Pi 1, Raspberry Pi Zero/W).
- **armv5 / arm / arm32**: Старая архитектура, встречающаяся в ранних встраиваемых системах.
</details>

## Языки

- Английский
- Фарси
- Китайский
- Русский
- Вьетнамский
- Испанский
- Индонезийский

## Возможности

- Мониторинг состояния системы
- Поиск по всем входящим подключениям и клиентам
- Тёмная/светлая тема
- Поддержка мультипользовательского и мультипротокольного режима
- Поддержка протоколов: VMess, VLESS, Trojan, Shadowsocks, Dokodemo-door, Socks, HTTP, wireguard
- Поддержка протоколов XTLS: RPRX-Direct, Vision, REALITY
- Статистика трафика, ограничение трафика, ограничение по дате истечения
- Настраиваемые шаблоны конфигураций Xray
- Поддержка HTTPS для панели (домены + SSL)
- Поддержка "одним кликом" получения SSL-сертификата и автоматического продления
- Дополнительные настройки конфигурации через панель
- Исправленные маршруты API (настройки пользователей будут создаваться через API)
- Поддержка изменений конфигураций различных параметров из панели
- Экспорт/импорт базы данных из панели

## Настройки по умолчанию

<details>
  <summary>Нажмите для просмотра настроек по умолчанию</summary>

### Информация

- **Порт:** 2053
- **Имя пользователя и пароль:** Генерируются случайно, если вы пропустите шаг изменения.
- **Путь к базе данных:**
    - /etc/x-ui/x-ui.db
- **Путь к конфигу Xray:**
    - /usr/local/x-ui/bin/config.json
- **Путь к веб-панели без SSL:**
    - http://ip:2053/panel
    - http://домен:2053/panel
- **Путь к веб-панели с SSL:**
    - https://домен:2053/panel

</details>

## [Настройка WARP](https://gitlab.com/fscarmen/warp)

<details>
  <summary>Нажмите для деталей о настройке WARP</summary>

#### Использование

Если вы хотите использовать маршрутизацию через WARP до версии v2.1.0, выполните следующие шаги:

**1.** Установка WARP в режиме **SOCKS Proxy**:

```sh
bash <(curl -sSL https://raw.githubusercontent.com/hamid-gh98/x-ui-scripts/main/install_warp_proxy.sh)
```

**2.** Если вы уже установили warp, вы можете удалить его:

```sh
warp u
```

**3.** Включите нужные настройки в панели.

Возможности конфигурации:
- Блокировка рекламы
- Маршрутизация Google + Netflix + Spotify + OpenAI (ChatGPT) через WARP
- Исправление ошибки Google 403

</details>

## Ограничение по IP

<details>
  <summary>Нажмите для деталей об ограничении по IP</summary>

#### Использование

**Примечание:** Ограничение по IP может работать некорректно при использовании IP-туннеля.

- Для версий до `v1.6.1`:

    - Ограничение по IP встроено в панель.

- Для версий `v1.7.0` и новее:

    - Чтобы ограничение по IP работало правильно, необходимо установить fail2ban и необходимые файлы:

        1. Введите команду `x-ui` в терминале.
        2. Выберите `IP Limit Management`.
        3. Выберите подходящие параметры в зависимости от ваших нужд.

    - Убедитесь, что в конфигурации Xray после v2.1.3 включён ./access.log:

  ```sh
    "log": {
    "access": "./access.log",
    "dnsLog": false,
    "loglevel": "warning"
    },
  ```

</details>

## Telegram Bot

<details>
  <summary>Нажмите для деталей о Telegram-боте</summary>

#### Использование

Веб-панель поддерживает ежедневную статистику трафика, уведомления о входе, резервные копии базы данных, состояние системы, информацию о клиенте и другие функции через Telegram-бота. Для использования необходимо настроить параметры бота в панели, включая:

- Telegram Token
- Admin Chat ID(ы)
- Время уведомления (синтаксис cron)
- Уведомление о дате истечения
- Уведомление о лимите трафика
- Резервное копирование базы данных
- Уведомление о загрузке ЦП

**Пример синтаксиса:**

- `30 * * * * *` - уведомление на 30-й секунде каждой минуты
- `0 */10 * * * *` - уведомление в первую секунду каждые 10 минут
- `@hourly` - раз в час
- `@daily` - раз в день (в полночь)
- `@weekly` - раз в неделю
- `@every 8h` - каждые 8 часов

### Возможности Telegram-бота

- Периодическая отчётность
- Уведомление о входе в панель
- Уведомление о превышении порога загрузки ЦП
- Предупреждение о сроке действия и трафике заранее
- Поддержка меню отчёта о клиентах, если указан Telegram-юзернейм клиента
- Поддержка телеграм-команды для проверки трафика по UUID (VMESS/VLESS) или паролю (TROJAN)
- Меню-ориентированный бот
- Поиск клиента по email (только для администратора)
- Проверка всех входящих подключений
- Проверка состояния сервера
- Проверка истощённых пользователей
- Получение резервной копии по запросу и периодические отчёты
- Поддержка нескольких языков

### Настройка Telegram-бота

- Начните работу с [Botfather](https://t.me/BotFather) в вашем Telegram:
  ![Botfather](./media/botfather.png)

- Создайте нового бота с помощью команды /newbot: Укажите имя и юзернейм бота (юзернейм должен заканчиваться на "bot").
  ![Create new bot](./media/newbot.png)

- Запустите созданного бота. Ссылка на вашего бота будет отображена:
  ![token](./media/token.png)

- Введите в панели настройки Telegram-бота:
  ![Panel Config](./media/panel-bot-config.png)

Вставьте ваш токен бота в поле №3.  
Вставьте ID пользователя в поле №4. Аккаунты Telegram с этими ID будут админами бота. (Можно указать несколько через запятую)

- Как узнать Telegram user ID? Используйте этого [бота](https://t.me/useridinfobot):
  ![User ID](./media/user-id.png)

</details>

## API маршруты

<details>
  <summary>Нажмите для деталей о маршрутах API</summary>

#### Использование

- `/login` с `POST` данными: `{username: '', password: ''}` для входа
- `/panel/api/inbounds` - базовый путь для дальнейших действий:

| Метод | Путь                                   | Действие                                     |
| :---: | -------------------------------------- | -------------------------------------------- |
| `GET` | `"/list"`                              | Получить все входящие                       |
| `GET` | `"/get/:id"`                           | Получить входящий по inbound.id             |
| `GET` | `"/getClientTraffics/:email"`          | Получить трафик клиента по email             |
| `GET` | `"/createbackup"`                      | Telegram-бот отправляет резервную копию      |
| `POST`| `"/add"`                               | Добавить входящий                            |
| `POST`| `"/del/:id"`                           | Удалить входящий                             |
| `POST`| `"/update/:id"`                        | Обновить входящий                            |
| `POST`| `"/clientIps/:email"`                  | IP-адреса клиента                            |
| `POST`| `"/clearClientIps/:email"`             | Очистить IP-адреса клиента                   |
| `POST`| `"/addClient"`                         | Добавить клиента к входящему                 |
| `POST`| `"/:id/delClient/:clientId"`           | Удалить клиента по clientId\*                |
| `POST`| `"/updateClient/:clientId"`            | Обновить клиента по clientId\*               |
| `POST`| `"/:id/resetClientTraffic/:email"`     | Сбросить трафик клиента                      |
| `POST`| `"/resetAllTraffics"`                  | Сбросить трафик для всех входящих            |
| `POST`| `"/resetAllClientTraffics/:id"`        | Сбросить трафик всех клиентов в одном входящем|
| `POST`| `"/delDepletedClients/:id"`            | Удалить исчерпавших лимит клиентов (-1: все) |
| `POST`| `"/onlines"`                           | Получить список онлайн-пользователей (email) |

\* - Поле `clientId` заполняется так:

- Для VMESS и VLESS: `client.id`
- Для TROJAN: `client.password`
- Для Shadowsocks: `client.email`

- [Документация API](https://documenter.getpostman.com/view/16802678/2s9YkgD5jm)
- [<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://app.getpostman.com/run-collection/16802678-1a4c9270-ac77-40ed-959a-7aa56dc4a415?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D16802678-1a4c9270-ac77-40ed-959a-7aa56dc4a415%26entityType%3Dcollection%26workspaceId%3D2cd38c01-c851-4a15-a972-f181c23359d9)

</details>

## Переменные окружения

<details>
  <summary>Нажмите для деталей о переменных окружения</summary>

#### Использование

| Переменная     | Тип                       | Значение по умолчанию |
| -------------- | ------------------------- | --------------------- |
| XUI_LOG_LEVEL  | `"debug"`, `"info"`, `"warn"`, `"error"` | `"info"` |
| XUI_DEBUG      | `boolean`                 | `false`              |
| XUI_BIN_FOLDER | `string`                  | `"bin"`              |
| XUI_DB_FOLDER  | `string`                  | `"/etc/x-ui"`        |
| XUI_LOG_FOLDER | `string`                  | `"/var/log"`         |

Пример:

```sh
XUI_BIN_FOLDER="bin" XUI_DB_FOLDER="/etc/x-ui" go build main.go
```

</details>

## Пример интерфейса

![1](./media/1.png)
![2](./media/2.png)
![3](./media/3.png)
![4](./media/4.png)
![5](./media/5.png)
![6](./media/6.png)
![7](./media/7.png)

## Особая благодарность

- [alireza0](https://github.com/alireza0/)

## Благодарности

- [Iran v2ray rules](https://github.com/chocolate4u/Iran-v2ray-rules) (Лицензия: **GPL-3.0**): _Улучшенные правила маршрутизации для v2ray/xray и v2ray/xray-клиентов с встроенными иранскими доменами, акцентом на безопасность и блокировку рекламы._
- [Vietnam Adblock rules](https://github.com/vuong2023/vn-v2ray-rules) (Лицензия: **GPL-3.0**): _Домен, размещённый во Вьетнаме, и блоклист для достижения максимальной эффективности для вьетнамских пользователей._

## Звёзды со временем

[![Stargazers over time](https://starchart.cc/MHSanaei/3x-ui.svg)](https://starchart.cc/MHSanaei/3x-ui)