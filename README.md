# VLESS Proxy Tester
Автоматизированный инструмент для тестирования VLESS прокси-серверов. Скрипт проверяет работоспособность прокси из списка VLESS-ссылок и сохраняет только рабочие конфигурации.

## Возможности

- **Автоматическое тестирование** - проверка работоспособности VLESS прокси
- **Поддержка основных протоколов**:
  - VLESS + TCP
  - VLESS + WebSocket (WS)
  - VLESS + gRPC
  - VLESS + HTTP/2
  - VLESS + REALITY
- **Умный парсинг** - автоматическое извлечение параметров из VLESS-ссылок
- **Детальное логирование** - подробная информация о процессе тестирования
- **Автоматическое управление Xray** - запуск и остановка Xray для каждого теста

## Требования

- **ОС**: Linux, macOS, WSL
- **Зависимости**: 
  - `curl` - для проверки подключения
  - `xray-core` - бинарник должен находиться в той же папке

## Установка и использование

```bash
# Скачайте архив и распакуйте
unzip vless-proxy-tester.zip

# Перейдите в папку со скриптом
cd vless-proxy-tester

# Убедитесь, что xray бинарник исполняемый
chmod +x xray

# Формат: vless://uuid@server:port?params#Название_прокси

vless://12345678-1234-1234-1234-123456789012@example.com:443?security=tls&sni=example.com#Пример_прокси
vless://abcdefgh-1234-1234-1234-abcdefghijkl@server.com:443?security=reality&sni=google.com#REALITY_прокси

## Примечание:
В комплекте включен бинарник Xray для macOS. Для других операционных систем скачайте подходящую версию:

# AMD64
wget https://github.com/XTLS/Xray-core/releases/latest/download/Xray-linux-64.zip
unzip Xray-linux-64.zip xray -d ./

# ARM64
wget https://github.com/XTLS/Xray-core/releases/latest/download/Xray-linux-arm64-v8a.zip
unzip Xray-linux-arm64-v8a.zip xray -d ./

# Windows (через WSL)
wget https://github.com/XTLS/Xray-core/releases/latest/download/Xray-windows-64.zip
unzip Xray-windows-64.zip xray.exe -d ./

## Запуск тестирования

./vless-tester.sh

## После выполнения скрипт создает:

test-results.txt - детальные результаты тестирования каждого прокси
working-proxies.txt - список только рабочих VLESS-ссылок

## Пример использования
# Запуск тестирования
$ ./vless-tester.sh
[14:30:25] === VLESS Proxy Tester ===
[14:30:25] Найдено ссылок для тестирования: 3
[14:30:25] ========================================
[1/3]
[14:30:25] ========================================
[14:30:25] Тестирование: Пример_прокси
[14:30:25] Декодирование VLESS-ссылки...
[14:30:25] Парсинг:
[14:30:25]    UUID: '12345678-1234-1234-1234-123456789012'
[14:30:25]    Сервер: 'example.com'
[14:30:25]    Порт: '443'
[14:30:25]    Название: 'Пример_прокси'
[14:30:25]    Security: 'tls'
...

✅ РАБОТАЕТ - Пример_прокси
❌ НЕ РАБОТАЕТ - Неактивный_прокси
✅ РАБОТАЕТ - REALITY_прокси

========================================
✅ Найдено рабочих прокси: 2
📄 Список сохранен в: working-proxies.txt
