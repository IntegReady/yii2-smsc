SMSCenter
=========

��������� Yii2 ��� ������ � �������� smsc.ru (SMS-�����)

�������:
* �������� ������/���������� ��������� �� ����/��������� ������� ����� ��������
* �������� ������� ���������
* ��������� ��������� ��������
* �������� �������
* ��������� ���������� �� ��������� �� ������

����������� ���������� � Yii2

***

���������� ����� ������� �������� (� ������� �������� ��-���������):

```php
'components' => [
    'SMSCenter' => [
        'class' => 'nikitich\smsc\SMSCenter',
        'login' => 'YourLogin',
        'password' => 'YourPa$$w0rd',
        'useSSL' => false,
        'options' => [
            'sender' => 'SenderName',   // ��� �����������
            'translit', // ���������� �� ��������� � �������� (self::TRANSLIT_NONE)
            'charset',  // ��������� ������� � ������ (self::CHARSET_UTF8)
            'fmt',      // ������ ������ ������� (self::FMT_JSON)
            'type',     // ��� ��������� (self::MSG_SMS), ������ push, ping, hlr � ������
            'cost',     // ����������� �� ��������� (self::COST_NO)
            'time',     // ����� �������� ��������� (null)
            'tz',       // ������� ���� ��������� time (null)
        ],
    ],
]
```

***

������� �������������:
```php
<?php
// �������������
$smsc = Yii::$app->SMSCenter;

// �������� ���������
$smsc->send('+7991111111', '������, �������!', 'SuperIvan');
Yii::$app->SMSCenter->send('+7991111111', '������, �������!', 'SuperIvan');

// �������� ��������� �� 2 ������
Yii::$app->SMSCenter->send(['+7(999)1111111', '+7(999)222-22-22'], '������, �������!', 'SuperIvan');
Yii::$app->SMSCenter->send('+7(999)1111111,+7(999)222-22-22', '������, �������!', 'SuperIvan');

// �������� ������ ��������� �� ������ ������
Yii::$app->SMSCenter->sendMulti([
    ['+79991111111', "Text 1\nnew line"],
    '+79992222222' => 'Text 2',
]);

// ��������� ��������� ��������
Yii::$app->SMSCenter->getCost('7991111111,79992222222', '������ ����� 251 ��� ���, ����� � 201 ��� ��� �����.');

// ��������� ��������� �������� ������ ��������� �� ������ ������
Yii::$app->SMSCenter->getCostMulti([
    '79991111111' => 'Text 1',
    '79992222222' => 'Text 2',
]);

// ��������� �������
Yii::$app->SMSCenter->getBalance(), ' ���.'; // "72.2 ���."

// ��������� ���������� �� ���������
Yii::$app->SMSCenter->getOperatorInfo('7991111111');

// ��������� ������� ���������
Yii::$app->SMSCenter->getStatus('+7991111111', 6, SMSCenter::STATUS_INFO_EXT);

// �������� �������� ����
if (Yii::$app->SMSCenter->getChargingZone('+79991111111') == self::ZONE_RU) {
    ...
}
```

***

��������: Apache License, Version 2.0
