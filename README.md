# mephi-session-project-2026
Сессионный проект по дисциплине "Операционные системы семейства Unix"

## Информация о проекте
* Студент: Комышков Владислав
* ОС: Fedora 43
* Среда: VirtualBox
* Hostname: `mephi-2026.domain.local`
* Студенческий номер: `369895`

## 1. Управление сетью
### 1.1. Настройка статического IP и hostname
- Статический IP `192.168.1.100/24` на интерфейсе `enp0s3`
- Шлюз `192.168.1.1`, DNS `8.8.8.8`
- Hostname настроен через `hostnamectl`

### 1.2. Проверка сетевой связности
- Проверка связности: `ping` до `8.8.8.8` и `192.168.1.1`, результат сохранён в `network_check.txt`

## 2. Управление программным обеспечением
### 2.1. Установка пакетов из репозиториев
- Установлены пакеты: `nginx`, `tcpdump`, `libcap-ng-utils`

### 2.2. Установка локального RPM-пакета
- Локальный RPM-пакет `tcpdump` скачан через `dnf download` и установлен через `rpm -Uvh`
- Файл сохранён как `tcpdump.rpm`

## 3. Файловые системы и сервисы
### 3.1. Создание и монтирование файловой системы
- Второй диск `/dev/sdb` разбит, создан раздел `/dev/sdb1`
- Раздел отформатирован в `ext4` с меткой `MEPHI_DATA`
- Точка монтирования: `/data/mephi-web`
- Автомонтирование настроено через `/etc/fstab` по метке тома (`fstab.txt`)

### 3.2. Управление сервисами и журналирование
- Сервис `nginx` запущен и добавлен в автозагрузку (`enabled`, `active`)
- nginx настроен на отдачу страниц из `/data/mephi-web`
- Логи nginx сохранены в `nginx_recent_logs.txt`

## 4. Управление доступом
### 4.1. Дискреционное управление доступом (DAC)
- Создан пользователь `mephi-admin`, группа `mephi-devs`
- Владелец `/data/mephi-web`: `mephi-admin:mephi-devs`
- Права `2775` (setgid) — новые файлы наследуют группу `mephi-devs`
- Проверки сохранены в `permissions.txt` и `users_groups.txt`

### 4.2. Мандатное управление доступом (MAC) и Capabilities
- SELinux работает в режиме `Enforcing`
- Для `/data/mephi-web` установлен SELinux-контекст `httpd_sys_content_t` (`file_contexts.txt`, `selinux_status.txt`)
- Для `/usr/sbin/tcpdump` снят SUID-бит и установлены capabilities `cap_net_admin,cap_net_raw=ep` (`tcpdump_capabilities.txt`)

## 5. Аутентификация и тестирование
### 5.1. Ограничение входа для root
- Вход root запрещён через PAM (`pam_listfile.so`, файл `/etc/ssh/denied_users`) для `/etc/pam.d/login` и `/etc/pam.d/sshd`
- В `/etc/ssh/sshd_config` установлено `PermitRootLogin no`

### 5.2. Тестирование настройки рабочей станции
- В `/data/mephi-web/index.html` размещена страница с текстом `Hello from Student: 369895`
- `curl http://localhost` и `curl http://192.168.1.100` возвращают `Hello from Student: 369895` (`curl_output.txt`)
- Скриншот работы nginx сохранён в `mephi-nginx-screenshot.png`

## Артефакты проекта
| Файл | Раздел | Описание |
|---|---|---|
| `project_history.txt` | Все | История выполненных команд |
| `network_check.txt` | 1.2 | Результаты ping |
| `nginx_recent_logs.txt` | 3.2 | Логи nginx |
| `fstab.txt` | 3.1 | Автомонтирование |
| `selinux_status.txt` | 4.2 | Режим SELinux |
| `file_contexts.txt` | 4.2 | Контекст SELinux |
| `tcpdump_capabilities.txt` | 4.2 | Capabilities tcpdump |
| `permissions.txt` | 4.1 | Права и владелец |
| `users_groups.txt` | 4.1 | Пользователи и группы |
| `index.html` | 5.2 | Web-страница |
| `curl_output.txt` | 5.2 | Результат curl |
| `mephi-nginx-screenshot.png` | 5.2 | Скриншот работы nginx |
| `tcpdump.rpm` | 2.2 | RPM-пакет tcpdump |

## Репозиторий
https://github.com/vladislav-gh-dump/mephi-session-project-2026
