# Прототипы ботов-викторин для Telegram и ВКонтакте с базой данных Redis
### Автор проекта: Алексей Свирин, телеграм — [@svirin](https://telegram.me/svirin)
### Цель проекта: создание прототипов ботов-викторин для мессенджера Телеграм и социальной сети ВКонтакте

# Как установить
### Этап 1. Получить все авторизационные ключи
#### Этап 1.1 Для запуска бота в Телеграме необходимо:
1) Создать бота для пользователй в telegram через [Отца ботов](https://telegram.me/BotFather) и взять токен для авторизации.
2) Создать бота для сервисных сообщений в telegram через [Отца ботов](https://telegram.me/BotFather) и взять токен для авторизации.
3) Узнать свой ID через [специального бота](https://telegram.me/userinfobot).

#### Этап 1.2 Для запуска бота во Вконтакте необходимо:
1) Создать бота для сервисных сообщений в telegram через [Отца ботов](https://telegram.me/BotFather) и взять токен для авторизации.
2) [Создать сообщество](https://vk.com/groups?tab=admin) или выбрать из уже созданных.
3) Взять сервисный ключ в разделе "Управление" на вкладке "Работа с API"
4) Разрешить отправку сообщений на вкладке "Сообщения"
5) Перейти в "Настройки для бота", “Возможности ботов”. Там же нужно добавить кнопку "Начать".

### Этап 2. Установить переменные окружения
1) REDIS_HOST — Host базы данных Redis;
2) REDIS_PORT — Port базы данных Redis;
3) REDIS_PASSWORD — Пароль базы данных Redis;
4) REDIS_DB — Номер базы данных Redis, по умолчанию ставить 0;
5) TELEGRAM_TOKEN — токен для авторизации бота в Телеграме;
6) VK_API_TOKEN — токен для авторизации в группе ВКонтакте.

Для пуктов 7 и 8 прочитайте примечание по запуску.  
7) PATH_TO_FILE — путь до файла с вопросами и ответами;  
8) ENCODING_FILE — кодировка файла с вопросами и ответами.

### Этап 3. Запустить бота 
#### Пример запуска в консоли
```python
python3 tg-bot.py
```

# Требования к окружению
Все требуемые модули указаны в файле requirements.txt  
Для установки запустите команду:
```python
python3 pip install -r requirements.txt
```

# Как сделать словарь для ботов
Так как каждый файл с бозой вопросов и ответов может быть сконфигурирован уникально, то не представляется возможности сделать универсальное решение по формированию словаря.
Словарь должен быть такого вида:
```python
{'Вопрос 1': 'ответ 1', 'Вопрос 2': 'ответ 2', 'Вопрос 3': 'ответ 3'}
```
Пример кода, который формирует словарь по моим файлам находится в файле [handler_dictionary.py](https://github.com/asvirin/quiz-bots/blob/master/handler_dictionary.py). Из этого файла вызывается функция для формирования словаря в ботах. Функция на вход принимает путь до файла, который нужен для формирования словаря, и кодировку файла для корректного считывания информации. Если вы планируете использовать сырой файл для формирования словаря, то вам скорее всего придется переписать алгоритм обработки под ваш файл.

# Требования к запуску на Heroku
Для запуска на Heroku необходимо:
1) Файл Procfile. В файле Procfile прописано какой файл нужно запускать на Heroku;
2) Файл Pipfile. В файлах Pipfile и reqirements.txt указаны необходимые модули для работы бота;
3) В разделе Settings добавить новый [Buildpack](https://github.com/elishaterada/heroku-google-application-credentials-buildpack);
4) В раздел Config Vars добавить все переменные окружения.
