# Спринт 2: Расследование инцидента с фишингом и компрометацией контроллера домена

## Описание
Расследование целевой атаки на хост `adds.demo.lab` (IP `10.0.0.10`). Атака началась с фишингового письма с вредоносным вложением `Salary_Update.exe`, что привело к закреплению в системе, эксфильтрации конфиденциальных данных и сокрытию следов.

## Цели
- Проанализировать фишинговое письмо и вредоносное вложение.
- Провести сбор артефактов в Velociraptor (процессы, сеть, задачи, реестр, MFT).
- Создать кейс в TheHive с индикаторами компрометации.
- Обогатить индикаторы через Cortex (VirusTotal, AbuseIPDB).
- Сопоставить атаку с MITRE ATT&CK.
- Разработать рекомендации по локализации и устранению инцидента.

## Инструменты
- **Velociraptor** - сбор артефактов (Pslist, LocalHashes, Netstat, TaskScheduler, BinaryHunter, EventLogs, MFT).
- **TheHive** - создание кейса инцидента.
- **Cortex / VirusTotal / AbuseIPDB** - обогащение индикаторов.
- **MITRE ATT&CK** - классификация техник.

## Результаты
### Выявлены индикаторы компрометации (IoC):
- **Email:** `support@deemo.lab`
- **Домен:** `deemo.lab` (typosquatting)
- **Вложение:** `Salary_Update.exe` (MD5: `236420e9795b30db8bf9e7db4b74610e`, SHA-1: `7fcf116e32d0685de0b766d0342d1001dc81657`, SHA-256: `5cbf2f4b4a57bcac660c79772401077764f60e85a5123a7e311859a211abb9c1`)
- **C2-сервер:** `101.99.90.131:443` (HTTPS)

### Обнаружены механизмы закрепления (Persistence):
- Задача в Task Scheduler: `SystemHealthMonitor`
- Ключ автозагрузки в реестре: `WindowsUpdate`

### Скомпрометированы конфиденциальные документы:
- `Salaries_2024.xlsx`
- `Budget_2025.xlsx`
- `Financial_Report.xlsx`  
(скопированы в `C:\Windows\Temp\staging`)

### Выявлены признаки сокрытия следов:
- Очистка журналов Security (Event ID 1102), System, Application, PowerShell (Event ID 104).

### Классифицированы техники MITRE ATT&CK:
 Техника Название Этап
T1566.001 Spearphishing Attachment Initial Access
T1204.002 Malicious File Execution
T1059.001 PowerShell Execution
T1053.005 Scheduled Task Persistence
T1547.001 Registry Run Keys Persistence
T1074 Data Staged Collection
T1071.001 Web Protocols C2
T1070.001 Clear Windows Event Logs Defense Evasion

### Хронология по Kill Chain:
1. **Reconnaissance** — сбор информации.
2. **Weaponization** — подготовка вредоноса и письма.
3. **Delivery** — отправка письма.
4. **Exploitation** — запуск вложения пользователем.
5. **Installation** — запуск PowerShell, скриптов, создание задач и ключей.
6. **Command & Control** — HTTPS-соединение с C2.
7. **Actions on Objectives** — эксфильтрация документов.

### Рекомендации:
- **Немедленно:** изоляция хоста, блокировка IP и домена, сброс паролей.
- **Краткосрочно:** удаление вредоносных файлов и задач, настройка мониторинга.
- **Долгосрочно:** усиление Email Security, AppLocker, сетевой сегментации и логирования.

## Файлы
- `report.pdf` — полный отчёт.
- `screenshots/` — скриншоты артефактов Velociraptor, TheHive, VirusTotal.
