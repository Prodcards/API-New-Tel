![](https://github.com/prodcards/API-New-Tel/blob/main/logo.svg)
# Группа методов для управления компанией в контексте абонента «Нью-Тел» (company/*)

Получение информации о компании: текущее состояние, информация о сотрудниках, номерах телефонов, тарифах, расходах и пр.

Доступные методы:

[Получение информации о состоянии компании-абонента](#1)

Получение информации из профиля компании

Получение информации о сотрудниках компании

Получение списка сотрудников компании

Получение информации из профиля сотрудника компании

Получение списков номеров телефонов компании

<a name="1"></a> 
## Получение информации о состоянии компании-абонента
Метод возвращает состояние компании-абонента «Нью-Тел»: баланс, статус и пр.
ВАЖНО: это единственный метод, который возвращает данные в случае, если аккаунт компании заблокирован, например, из-за недостатка средств на счёте!
### Наименование метода
company/get-state
### Параметры запроса
нет
### Ограничение запросов
стандартное
### Атрибуты ответа
|Артибут|Тип данных|Объект|Примечание|
|:------|:---:|:------:|----------------------------------------|
|state|object|?|Сведения о компании|
| - balance|decimal (10,2)|Нет|Текущий баланс компании в указанной валюте расчетов. Может принимать отрицательные значения. Null, если информация о балансе не предоставляется|
|------------------|---|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| credit           | – | кредит для компании, целое или десятичное число (максимум 2 знака после запятой) или null, если информация о кредите не предоставляется                                            |
| currency         | – | валюта расчётов, строка, возможные значения: "RUB" – российский рубль, "EUR" – евро, "USD" – доллар США                                                                            |
| dayTrafficCost   | – | расходы за последние сутки                                                                                                                                                         |
| monthTrafficCost | – | расходы за последний месяц, число                                                                                                                                                  |
| status           | – | текущий статус аккаунта компании, строка, возможные значения: "active" – активен, "blocked" – заблокирован, "testing" – тестовый период, "suspended" – обслуживание приостановлено |

### Пример запроса
    URL
        https://api.new-tel.net/company/get-state
    HEAD
        Authorization: Bearer df9b7fg89n79...
        Content-Type: application/json
    BODY
        {}
### Пример ответа
    STATUS: 200 OK
     
    BODY
    {
	    "status": "success",
	    "data": {
    		"result": "success",
	    	"state": {
		    	"balance": -131,
			    "credit": 0,
			    "currency": "RUB",
			    "dayTrafficCost": 0,
			    "monthTrafficCost": 33.08,
			    "status": "active"
		    }
	    }
    }     
