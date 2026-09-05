# Спринт 1: Детектирование атак Brute Force, Kerberoasting, Port Scanning и DNS Tunneling



## Описание

Проведение учебных атак на тестовом стенде и анализ их следов в логах. Роль — SOC-аналитик (синяя команда).



## Цели

- Выполнить Brute Force (RDP), Kerberoasting, Port Scanning (Nmap), DNS Tunneling.

- Настроить обнаружение (iptables, Snort).

- Проанализировать логи Windows, Snort, syslog и DNS-трафик.

- Сформулировать рекомендации по защите.



## Инструменты

- Kali Linux (Hydra, Impacket, Nmap)

- Windows Server 2019 (AD, DNS, Security Log)

- Ubuntu 22.04 (iptables, Snort)

- Wireshark



## Результаты

Обнаружены и задокументированы:

- Event ID 4625, 4624 (Brute Force)

- Event ID 4769 (Kerberoasting)

- PORTSCAN DETECTED в syslog, алерты Snort

- Аномальные DNS-запросы (туннель)



Подробности — в полном отчёте (`report.pdf`) и скриншотах (`screenshots/`).



## Вывод

Проект позволил освоить детектирование распространённых атак и настройку средств мониторинга. Навыки применимы в реальной SOC-работе.

