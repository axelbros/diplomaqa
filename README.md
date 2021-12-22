# Дипломный проект профессии «Тестировщик ПО»

# Веб-сервис "Путешествие дня"

Дипломный проект представляет собой автоматизацию тестирования комплексного сервиса, взаимодействующего с СУБД и API
Банка.

Приложение предлагает купить тур по определённой цене с помощью двух способов:

1. Оплата по дебетовой карте
2. Оплата по кредитной карте

Само приложение не обрабатывает данные по картам, а пересылает их банковским сервисам:

1. Сервису платежей - Payment Gate
2. Кредитному сервису - Credit Gate

Приложение в собственной СУБД сохраняет информацию о том, каким способом был совершён платёж и успешно ли он был
совершён.

---

## Начало работы

Github - склонировать проект себе на ПК для последующего запуска и тестирования.

Для запуска тестов на вашем ПК должно быть установлено следующее ПО:

- IntelliJ IDEA
- Git
- Docker Desktop
- Google Chrome (или другой браузер)

---

### Установка и запуск

1) Запускаем контейнеры из файла **docker-compose.yml** командой в терминале:

```
docker-compose up
```

и проверяем, что контейнеры запустились командой:

```
docker-compose ps
```

Ожидаемый статус контейнеров - **UP**

![](../untitled30/Screenshots/Containers.png)

2) Запускаем SUT командой в терминале:

- для MySQL:

```
java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" -jar artifacts/aqa-shop.jar
```

- для PostgreSQL:

```
java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/app" -jar artifacts/aqa-shop.jar
```

3) Запускаем авто-тесты командой в терминале:

- для MySQL:

```
./gradlew clean test "-Ddatasource.url=jdbc:mysql://localhost:3306/app"
```

- для PostgreSQL:

```
./gradlew clean test "-Ddatasource.url=jdbc:postgresql://localhost:5432/app"
```

Дождаться сообщения в терминале, которое будет означать, что приложение успешно запущено:

```
date time INFO 20036 --- [           main] ru.netology.shop.ShopApplication         : Started ShopApplication in 6.475 seconds (JVM running for 7.201)
```

Сервис будет доступен в браузере по адресу: _http://localhost:8080/_

4) Генерируем отчёт по итогам тестирования с помощью **Allure**. Отчёт автоматически откроется в браузере с помощью команды в терминале:

```
./gradlew allureServe
```

После генерации и работы с отчётом, останавливаем работу **allureServe** в терминале сочетанием клавиш _CTRL + C_ и
подтверждаем действие в терминале вводом _Y_.

Если необходимо перезапустить контейнеры, приложение или авто-тесты, нужно остановить работу сервисов в терминале
сочетанием клавиш _CTRL + C_ и перезапустить их, повторив шаги 1-3.

---

## Документация

- [План автоматизации тестирования](https://github.com/MVGIC/QA-Diploma/blob/master/Documentation/Plan.md)
- [Отчёт по итогам автоматизированного тестирования](https://github.com/MVGIC/QA-Diploma/blob/master/Documentation/Report.md)
- [Отчёт по итогам автоматизации](https://github.com/MVGIC/QA-Diploma/blob/master/Documentation/Summary.md)