[![](https://github.com/prodcards/API-New-Tel/blob/main/logo.svg)]
# Группа методов для управления компанией в контексте абонента «Нью-Тел» (company/*)

Получение информации о компании: текущее состояние, информация о сотрудниках, номерах телефонов, тарифах, расходах и пр.
Доступные методы:
Получение информации о состоянии компании-абонента
Получение информации из профиля компании
Получение информации о сотрудниках компании
Получение списка сотрудников компании
Получение информации из профиля сотрудника компании
Получение списков номеров телефонов компании
## Получение информации о состоянии компании-абонента
Метод возвращает состояние компании-абонента «Нью-Тел»: баланс, статус и пр.
ВАЖНО: это единственный метод, который возвращает данные в случае, если аккаунт компании заблокирован, например, из-за недостатка средств на счёте!
### Наименование метода
company/get-state
### Параметры запроса
нет
### Ограничение запросов
стандартное
### Данные ответа
объект state, содержащий свойства:
balance	–	текущий баланс компании, целое или десятичное число (максимум 2 знака после запятой) или null, если информация о балансе не предоставляется
credit	–	кредит для компании, целое или десятичное число (максимум 2 знака после запятой) или null, если информация о кредите не предоставляется
currency	–	валюта расчётов, строка, возможные значения: "RUB" – российский рубль, "EUR" – евро, "USD" – доллар США
dayTrafficCost	–	расходы за последние сутки
monthTrafficCost	–	расходы за последний месяц, число
status	–	текущий статус аккаунта компании, строка, возможные значения: "active" – активен, "blocked" – заблокирован, "testing" – тестовый период, "suspended" – обслуживание приостановлено
### Пример запроса
    

    URI
        https://api.new-tel.net/company/get-state
    HEAD
        Authorization: Bearer df9b7fg89n79...
        Content-Type: application/json
    BODY
        {}
### Пример ответа


     {
        "status":"success",
        "data":{
            "result":"success",
            "state":{
                 "balance":-131,
                 "credit":0,
                 "currency":"RUB",
                 "dayTrafficCost":0,
                 "monthTrafficCost":33.08,
                 "status":"active"
                        }
                   }
     }
Получение информации из профиля компании
Метод возвращает данные профиля компании: ID, наименование, сведения о регистрации и пр.
Наименование метода
company/get-profile-details
Параметры запроса
нет
Ограничение запросов
стандартное
Данные ответа
объект profileDetails, содержащий свойства:
id	–	ID компании, целое число
companyName	–	наименование организации, строка
registeredBy	–	наименование организации, создавшей аккаунт компании, строка или null, если аккаунт был создан при самостоятельной регистрации
registeredOn	–	время создания аккаунта компании, Unix timestamp
agreementNumber	–	номер договора, строка или null, если параметры договора недоступны
agreementDate	–	дата договора, строка или null, если параметры договора недоступны
Пример запроса
URI
https://api.new-tel.net/company/get-profile-details
HEAD
Authorization: Bearer df9b7fg89n79...
Content-Type: application/json
BODY
{}
Пример ответа
{
"status":"success",
"data":{
"result":"success",
"profileDetails":{
"id":7701,
"companyName":"Проверка системы",
"registeredBy":"ООО «Нью-Тел»",
"registeredOn":1607762100,
"agreementNumber":null,
"agreementDate":null
}
}
}
Получение информации о сотрудниках компании
Метод возвращает данные профилей сотрудников компании: имя, email, номера телефонов и пр.
Наименование метода
company/get-members
Параметры запроса
нет
Ограничение запросов
стандартное
Данные ответа
массив members – массив объектов, каждый из которых содержит свойства:
Id	–	ID сотрудника, число
Name	–	имя сотрудника, строка
Email	–	адрес электронной почты, строка
internalNumber	–	внутренний номер, строка или null, если внутренний номер не назначен
personalNumber	–	личный номер, строка или null, если личный номер не задан
timeZone	–	временная зона, строка
Пример запроса
URI
https://api.new-tel.net/company/get-members
HEAD
Authorization: Bearer df9b7fg89n79...
Content-Type: application/json
BODY
{}
Пример ответа
{
"status":"success",
"data":{
"result":"success",
"members":[
{
"id":9423,
"name":"Сергей",
"email":"prostoforce1995@mail.ru",
"internalNumber":"900",
"personalNumber":"79311110714",
"timeZone":"Europe/Moscow"
},
{
"id":9862,
"name":"Игорь",
"email":"shilovigor@new-tel.net",
"internalNumber":"303",
"personalNumber":null,
"timeZone":"Europe/Moscow"
},
{
"id":10185,
"name":"evgen",
"email":"boriso1155151@gmail.com",
"internalNumber":"902",
"personalNumber":"79311110537",
"timeZone":"Europe/Moscow"
}
]
}
}
Получение списка сотрудников компании
Метод возвращает список с именами всех сотрудников компании.
Наименование метода
company/get-members-list
Параметры запроса
нет
Ограничение запросов
стандартное
Данные ответа
массив membersList – список с именами сотрудников компании
Пример запроса
URI
https://api.new-tel.net/company/get-members-list
HEAD
Authorization: Bearer df9b7fg89n79...
Content-Type: application/json
BODY
{}
Пример ответа
{
"status": "success",
"data": {
"result": "success",
"membersList": [
"Иванов Иван",
"Петров Андрей"
]
}
}
Получение информации из профиля сотрудника компании
Метод возвращает данные профиля сотрудника компании: имя, email, номера телефонов и пр.
Наименование метода
company/get-member-details
Параметры запроса
name	–	имя сотрудника компании, строка длиной не менее 1 символа
Ограничение запросов
стандартное
Данные ответа
объект memberDetails, содержащий свойства:
Id	–	Id сотрудника, число
name	–	имя сотрудника, строка
email	–	адрес электронной почты, строка
internalNumber	–	внутренний номер, строка или null, если внутренний номер не назначен
personalNumber	–	личный номер, строка или null, если личный номер не задан
timeZone	–	временная зона, строка
Если сотрудника компании с именем, указанном в параметре запроса name нет, будет сформировано сообщение об ошибке "Member not found".
Пример запроса
URI
https://api.new-tel.net/company/get-member-details
HEAD
Authorization: Bearer df9b7fg89n79…
Content-Type: application/json
BODY
{'name' => 'Игорь'}
Пример ответа
{
"status":"success",
"data":{
"result":"success",
"memberDetails":{
"id":9862,
"name":"Игорь",
"email":"shilovigor@new-tel.net",
"internalNumber":"303",
"personalNumber":null,
"timeZone":"Europe/Moscow"
}
}
}
Получение списков номеров телефонов компании
Метод возвращает списки номеров телефонов компании, сгруппированных по типу.
Наименование метода
company/get-numbers
Параметры запроса
нет
Ограничение запросов
стандартное
Данные ответа
объект numbers, содержащий массивы:
external	–	список внешних номеров телефонов. Номера представляют собой строку.
internal	–	список внутренних номеров телефонов. Номера представляют собой строку.
virtual	–	список виртуальных номеров телефонов. Номера представляют собой строку.
Пример запроса
URI
https://api.new-tel.net/company/get-numbers
HEAD
Authorization: Bearer df9b7fg89n79…
Content-Type: application/json
BODY
{}
Пример ответа
{
"status":"success",
"data":{
“result":"success",
"numbers":{
"external":[
"74951089830",
"74956408992",
"74997540086",
"78007776117",
"79311110537",
"79311110714"
],
"internal":[
"100",
"101",
"303",
"900",
"902"
],
"virtual":[
]
}
}
}
Группа методов для управления аккаунтом авторизованного пользователя (user/*)
Получение информации из профиля пользователя, смена логина, пароля, ключей для взаимодействия по API и пр.
Доступные методы:
Получение информации из профиля авторизованного пользователя
Получение информации из профиля авторизованного пользователя
Метод возвращает данные профиля авторизованного пользователя-сотрудника компании: имя, email, номера телефонов.
Наименование метода
user/get-profile-details
Параметры запроса
нет
Ограничение запросов
стандартное
Данные ответа
объект profileDetails, содержащий свойства:
name	–	имя сотрудника, строка
email	–	адрес электронной почты, строка
internalNumber	–	внутренний номер, строка или null, если внутренний номер не назначен
personalNumber	–	личный номер, строка или null, если личный номер не задан
timeZone	–	временная зона, строка
Пример запроса
URI
https://api.new-tel.net/company/get-profile-details
HEAD
Authorization: Bearer df9b7fg89n79…
Content-Type: application/json
BODY
{}
Пример ответа
{
"status": "success",
"data": {
"result": "success",
"profileDetails": {
"name": “Иванов Иван”,
"email": "ivanov@company.org",
"internalNumber": "100",
"personalNumber": "79991234567",
"timeZone": "Europe/Moscow"
}
}
}
