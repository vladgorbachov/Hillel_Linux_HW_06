# Systemd Service and Slice - Homework 06
## Опис завдання

Створення власного systemd service, який працює у фоновому режимі, та slice unit з лімітами ресурсів.

## Структура проекту
.
├── systemd/
│   ├── hillei_hw.slice      # Slice з лімітами CPU та Memory
│   └── myworker.service      # Фоновий сервіс
├── scripts/
│   └── worker.sh             # Скрипт воркера
└── README.md
## Встановлення

### 1. Копіюємо файли
```bash
# Копіюємо скрипт
sudo cp scripts/worker.sh /opt/myservice/
sudo chmod +x /opt/myservice/worker.sh

# Копіюємо конфігурації systemd
sudo cp systemd/hillei_hw.slice /etc/systemd/system/
sudo cp systemd/myworker.service /etc/systemd/system/
# Перезавантажуємо конфігурацію
sudo systemctl daemon-reload

# Запускаємо slice та сервіс
sudo systemctl start hillei_hw.slice
sudo systemctl start myworker.service

# Автозапуск
sudo systemctl enable myworker.service
# Статус сервісу
systemctl status myworker.service

# Статус slice
systemctl status hillei_hw.slice

# Перевірка лімітів
systemctl show hillei_hw.slice | grep -E "(CPUQuota|MemoryMax)"

# Моніторинг
systemd-cgtop
