# Руководство по вычислению HMAC в командной строке с использованием OpenSSL

Этот репозиторий содержит инструкции и программы для вычисления HMAC в командной строке с помощью OpenSSL.

## Вычисление HMAC с помощью команды OpenSSL dgst

### Предварительные требования
- Установленный OpenSSL на вашей системе

### Шаги
1. Сгенерируйте тестовый файл:
    ```bash
    seq 20000 > somefile.txt
    ```
2. Сгенерируйте секретный ключ:
    ```bash
    openssl rand -hex 32
    ```
3. Вычислите HMAC с помощью команды `openssl dgst`:
    ```bash
    openssl dgst -sha256 -hmac <ключ-256bit> somefile.txt
    ```

    или 

    ```bash
    openssl dgst -sha-256 -mac HMAC -macopt hexkey:<ключ-256bit> somefile.txt 
    ```


### Примечания
- Для передачи секретного ключа в шестнадцатеричном виде используйте флаг `-macopt hexkey`.

## Вычисление HMAC с помощью новой подкоманды OpenSSL mac

### Шаги
1. Вычислите HMAC с помощью подкоманды `openssl mac`:
    ```bash
    openssl mac -macopt hexkey:<ключ-256bit> -digest sha256 -in somefile.txt HMAC
    ```

### Примечания
- Обратите внимание, что значение HMAC может быть представлено в немного другом формате.

## Вычисление HMAC из программы

### Программа hmac
Программа `hmac` вычисляет HMAC-SHA-256. Она принимает два аргумента в командной строке:
1. Имя входного файла
2. Секретный ключ в шестнадцатеричном виде

### Шаги
1. Запустите программу `hmac` с указанием файла и ключа:
    ```bash
    python3 hmac somefile.txt <ключ-256bit>
    ```

## Заключение
Этот репозиторий демонстрирует различные способы вычисления HMAC в командной строке с использованием OpenSSL. Примеры показывают как использовать как старую подкоманду `openssl dgst`, так и новую подкоманду `openssl mac`, а также как вычислять HMAC из пользовательской программы.
