# Краткое руководство по симметричному шифрованию и хешированию с использованием OpenSSL

Этот репозиторий содержит инструкции и примеры программ для выполнения операций симметричного шифрования и хеширования с помощью библиотеки OpenSSL.

## 1. Шифрование с помощью командной строки OpenSSL и пользовательской программы

### Операции:
- Генерация ключей
- Шифрование файлов в различных режимах
- Расшифровка файлов
- Шифрование файлов в режиме GCM
- Хранение IV и аутентификационного жетона в зашифрованном файле

### Примеры:
- Инструкции по использованию командной строки OpenSSL для шифрования и расшифровки файлов
- Пример программы для шифрования файлов с использованием библиотеки OpenSSL в режиме GCM

## 2. Вычисление хеш-значения

### Операции:
- Вычисление хеш-значения файла с помощью подкоманды `openssl dgst`

### Примеры:
- Инструкции и примеры для вычисления хеш-значения файла в командной строке
- Пример программы для вычисления хеш-значения SHA3-256 из файла

Этот репозиторий предоставляет простые инструкции и примеры кода для выполнения операций шифрования и хеширования с использованием библиотеки OpenSSL как из командной строки, так и из пользовательской программы.

## 3. Вычисление MAC и HMAC

### Операции:
- Вычисление HMAC с помощью подкоманды `openssl dgst` и новой подкоманды `openssl mac`

### Примеры:
- Инструкции и примеры для вычисления HMAC (код аутентификации сообщения с использованием хэш-функции) в командной строке
- Пример программы для вычисления HMAC-SHA-256 из файла

## 4. Формирование ключа шифрования из пароля

### Операции:
- Создание ключа шифрования из пароля с использованием подкоманды OpenSSL KDF
- Использование KDF для генерации стойких к полному перебору ключей

### Примеры:
- Инструкции и примеры для создания ключа шифрования из пароля с использованием новой подкоманды OpenSSL KDF



