SMSCenter
=========

Компонент Yii2 для работы с сервисом smsc.ru (SMS-Центр)
сделано на базе библиотеки https://github.com/jhaoda/SMSCenter

Функции:
* отправка одного/нескольких сообщений на один/несколько номеров одним запросом
* проверка статуса сообщений
* получение стоимости рассылки
* проверка баланса
* получение информации об операторе по номеру

Минимальные требования — Yii2

***

Допустимые ключи массива настроек (в скобках значения по-умолчанию):

```php
'components' => [
    'SMSCenter' => [
        'class' => 'integready\smsc\SMSCenter',
        'login' => 'YourLogin',
        'password' => 'YourPa$$w0rd',
        'useSSL' => false,
        'options' => [
            'sender' => 'SenderName',   // имя отправителя
            'translit', // кодировать ли сообщения в транслит (self::TRANSLIT_NONE)
            'charset',  // кодировка запроса и ответа (self::CHARSET_UTF8)
            'fmt',      // формат ответа сервера (self::FMT_JSON)
            'type',     // тип сообщения (self::MSG_SMS), замена push, ping, hlr и прочих
            'cost',     // запрашивать ли стоимость (self::COST_NO)
            'time',     // время отправки сообщения (null)
            'tz',       // часовой пояс параметра time (null)
        ],
    ],
]
```

***

Примеры использования:
```php
<?php

use integready\smsc\SMSCenter;

// Инициализация
$smsc = Yii::$app->SMSCenter;

// Отправка сообщения
$smsc->send('+7991111111', 'Превед, медведы!', 'SuperIvan');
Yii::$app->SMSCenter->send('+7991111111', 'Превед, медведы!', 'SuperIvan');

// Отправка сообщения на 2 номера
Yii::$app->SMSCenter->send(['+7(999)1111111', '+7(999)222-22-22'], 'Превед, медведы!', 'SuperIvan');
Yii::$app->SMSCenter->send('+7(999)1111111,+7(999)222-22-22', 'Превед, медведы!', 'SuperIvan');

// Отправка разных сообщений на разные номера
Yii::$app->SMSCenter->sendMulti([
    ['+79991111111', "Text 1\nnew line"],
    '+79992222222' => 'Text 2',
]);

// Получение стоимости рассылки
Yii::$app->SMSCenter->getCost('7991111111,79992222222', 'Начало около 251 млн лет, конец — 201 млн лет назад.');

// Получение стоимости рассылки разных сообщений на разные номера
Yii::$app->SMSCenter->getCostMulti([
    '79991111111' => 'Text 1',
    '79992222222' => 'Text 2',
]);

// Получение баланса
Yii::$app->SMSCenter->getBalance(); // ' руб.'; // "72.2 руб."

// Получение информации об операторе
Yii::$app->SMSCenter->getOperatorInfo('7991111111');

// Получения статуса сообщения
Yii::$app->SMSCenter->getStatus('+7991111111', 6, SMSCenter::STATUS_INFO_EXT);

// Проверка тарифной зоны
if (Yii::$app->SMSCenter->getChargingZone('+79991111111') == SMSCenter::ZONE_RU) {
    // ...
}
```

***

Лицензия: Apache License, Version 2.0
