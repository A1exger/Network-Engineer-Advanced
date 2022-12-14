# Реализация DHCPv4/6
### Топология
![Topoligie](https://user-images.githubusercontent.com/99610266/170830737-e54e84c2-d91f-4205-abf9-ea12cc18b705.png)
### Настройка базовойконфигурации на маршрутизаторах выполнена.
### 1. Настройка интерфейсов и маршрутизации для обоих маршрутизаторов.
#### Настроены интерефейсы на маршрутизаторах согласно таблице.
#### Настроен маршрут по умолчанию.
#### Cheking access
### ![1](https://user-images.githubusercontent.com/99610266/170831098-2daeebc8-d001-4d24-954c-9c0f8298b5dc.png)
#### Пинг успешно доходит до интерефейсов Gi0/0/1 с обоих маршрутизаторов.
### Проверка назначения адреса SLAAC от R1.
![2](https://user-images.githubusercontent.com/99610266/170831332-3029cbfa-7dca-4f6e-86b2-f50f3f2c1819.png)
#### Question: Откуда взялсась часть адреса с идентификатором хоста?
#### Часть хоста автоматически назначилась из сети настроенной на порту маршрутизатора R1 Gi0/0/1 2001:db8:acad:1::1/64
### 2. Настройка и проверка сервера DHCPv6 на R1
#### Более подробно изучите конфигурацию PC-A.
![3](https://user-images.githubusercontent.com/99610266/170831777-da961252-50c5-4d22-bee6-b06e609ef9f5.png)
#### Настройте R1 для предоставления DHCPv6 без состояния для PC-A.
#### Настройки были произведены. Т.к на Gi0/0/1 я упустил момент и не настроил link local адрес на скриншоте выше отображается некорректная информация по некоторым пунктам.
#### После настройки и добавления link-local адреса результат на скрине внизу.
![4](https://user-images.githubusercontent.com/99610266/170832394-599160e6-03a8-4b23-80b6-dab4d207a03c.png)
#### Тестирование подключения с помощью пинга IP-адреса интерфейса G0/1 R2. Successfully.
![5](https://user-images.githubusercontent.com/99610266/170832462-0101644f-327d-4e92-b2a5-75d6d8f0e1bc.png)
### 3. Настройка сервера DHCPv6 с сохранением состояния на R1
#### Настройка произведена.
![6](https://user-images.githubusercontent.com/99610266/170832806-a740c858-4e54-4d1d-84c2-ba4328e8858a.png)
### 4. Настройка и проверка ретрансляции DHCPv6 на R2.
#### Включите PC-B и проверьте адрес SLAAC, который он генерирует.
![7](https://user-images.githubusercontent.com/99610266/170832993-2efc287f-ad4a-41ac-a820-d10d033539fa.png)
#### При настройке выяснилось что одной команды нет в CPT.
![8](https://user-images.githubusercontent.com/99610266/170833574-e4882366-a66a-4d93-8ea0-fff0577a56d4.png)
#### Поэтому я просто также настроил на втором роутере DHCP и пропинговал с ПК-Б адрес ПК-А. 
![9](https://user-images.githubusercontent.com/99610266/170834045-7241157c-3e41-4a5d-9292-2469280cb0fa.png)
#### Получается что просто 2 отдельных DHCP сервера в сети.
#### Проверил также пинг до Gi0/0/1 интерфейса на R1.
![10](https://user-images.githubusercontent.com/99610266/170834168-5ed1df41-896f-4b41-85a6-912465f4afcf.png)

## Но!
#### На этом все не заканчивается. Все таки название лабораторной Реализация DHCPv4/6.
#### DHCPv6 настроил, но не было ни слова про 4-ю версию...это было странно да. После расследования и поиска зацепок была обнаружена отдельным файлом лабораторная по настройке DHCPv4. Теперь предстоит настройка DHCPv4.
# Реализация DHCPv4
## Создание схемы адресации.
#### Подсеть сети 192.168.1.0/24 в соответствии со следующими требованиями:
### a.	Одна подсеть «Подсеть A», поддерживающая 58 хостов Vlan 100
### b.	Одна подсеть «Подсеть B», поддерживающая 28 хостов Vlan 200
### c.	Одна подсеть «Подсеть C», поддерживающая 12 узлов R2 int Gi0/0/1
#### ![11](https://user-images.githubusercontent.com/99610266/170859387-82173549-e902-482f-9e1f-1a3a4d39ab8d.png)
#### Настройте G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов
### ![12](https://user-images.githubusercontent.com/99610266/170860594-66d7564b-b918-4afd-90ba-d114b60f4f4c.png)
#### Настройка произведена пинги доходят.
#### Почему интерфейс F0/5 указан в VLAN 1? Потому что vlan 1 по умолчанию.
## Настройка и проверка двух серверов DHCPv4 на R1
### Проверка конфигурации сервера DHCPv4
#### show ip dhcp server statistics команда отсутствует в CPT.
![13](https://user-images.githubusercontent.com/99610266/170874865-a4ab25e8-d272-4bf7-b02a-8e5135a5062a.png)
### Попытка получить IP-адрес от DHCP на PC-A
#### Адрест получен.
#### Проверьте подключение с помощью пинга IP-адреса интерфейса R0 G0/0/1. Пинг доходит.
#### ![14](https://user-images.githubusercontent.com/99610266/170875163-a168a087-63a2-46a2-90ff-c12c02adf7dc.png)
## Настройка и проверка DHCP-ретрансляции на R2
#### Настройка R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1
#### Настройка произведена
![15](https://user-images.githubusercontent.com/99610266/171986640-d1218789-d449-4789-9757-1802adc07ffe.png)
#### IP адрес получен пинги доходят.
![16](https://user-images.githubusercontent.com/99610266/171986771-23ba7360-a52e-4c41-9ae0-9332913533ef.png)
![17](https://user-images.githubusercontent.com/99610266/171986775-32f07196-70fb-4956-9e25-c84276977349.png)
