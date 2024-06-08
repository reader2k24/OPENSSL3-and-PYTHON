# Руководство по генерации и проверке сертификатов с использованием OpenSSL

Этот репозиторий содержит инструкции по генерации самоподписанных и несамоподписанных сертификатов, а также их проверке с использованием OpenSSL. Включены команды для создания ключей и сертификатов, а также примеры программ для подписи и проверки сертификатов.

## Генерация самоподписанного сертификата

### Шаги

1. Сгенерируйте пару ключей ED448:
    ```bash
    openssl genpkey -algorithm ED448 -out root_keypair.pem
    ```

2. Проверьте созданный ключ:
    ```bash
    openssl pkey -in root_keypair.pem -noout -text
    ```

3. Сгенерируйте CSR-запрос:
    ```bash
    openssl req -new -subj "/CN=Root CA" -addext "basicConstraints=critical,CA:TRUE" -key root_keypair.pem -out root_csr.pem
    ```

4. Проверьте содержимое CSR-запроса:
    ```bash
    openssl req -in root_csr.pem -noout -text
    ```

5. Сгенерируйте самоподписанный сертификат:
    ```bash
    openssl x509 -req -in root_csr.pem -copy_extensions copyall -key root_keypair.pem -days 3650 -out root_cert.pem
    ```

6. Проверьте содержимое самоподписанного сертификата:
    ```bash
    openssl x509 -in root_cert.pem -noout -text
    ```

## Генерация несамоподписанных сертификатов

### Шаги

1. Сгенерируйте пару ключей для промежуточного УЦ:
    ```bash
    openssl genpkey -algorithm ED448 -out intermediate_keypair.pem
    ```

2. Сгенерируйте CSR-запрос для промежуточного УЦ:
    ```bash
    openssl req -new -subj "/CN=Intermediate CA" -addext "basicConstraints=critical,CA:TRUE" -key intermediate_keypair.pem -out intermediate_csr.pem
    ```

3. Выпустите сертификат промежуточного УЦ, подписав его корневым сертификатом:
    ```bash
    openssl x509 -req -in intermediate_csr.pem -copy_extensions copyall -CA root_cert.pem -CAkey root_keypair.pem -days 3650 -out intermediate_cert.pem
    ```

4. Проверьте содержимое сертификата промежуточного УЦ:
    ```bash
    openssl x509 -in intermediate_cert.pem -noout -text
    ```

5. Сгенерируйте пару ключей для листового сертификата:
    ```bash
    openssl genpkey -algorithm ED448 -out leaf_keypair.pem
    ```

6. Сгенерируйте CSR-запрос для листового сертификата:
    ```bash
    openssl req -new -subj "/CN=Leaf" -addext "basicConstraints=critical,CA:FALSE" -key leaf_keypair.pem -out leaf_csr.pem
    ```

7. Выпустите листовой сертификат, подписав его сертификатом промежуточного УЦ:
    ```bash
    openssl x509 -req -in leaf_csr.pem -copy_extensions copyall -CA intermediate_cert.pem -CAkey intermediate_keypair.pem -days 3650 -out leaf_cert.pem
    ```

8. Проверьте содержимое листового сертификата:
    ```bash
    openssl x509 -in leaf_cert.pem -noout -text
    ```

## Проверка сертификатов в командной строке

### Шаги

1. Проверьте листовой сертификат с использованием корневого и промежуточного сертификатов:
    ```bash
    openssl verify -verbose -show_chain -trusted root_cert.pem -untrusted intermediate_cert.pem leaf_cert.pem
    ```

## Проверка сертификатов из программы

### Подготовка

1. Установите библиотеку `pyopenssl`:
    ```bash
    pip install pyopenssl
    ```

### Проверка сертификата

1. Запустите программу `x509-verify` для проверки листового сертификата:
    ```bash
    python3 x509-verify root_cert.pem intermediate_cert.pem leaf_cert.pem
    ```

2. Проверьте случай ошибки, запустив программу без промежуточного сертификата:
    ```bash
    python3 x509-verify root_cert.pem leaf_cert.pem leaf_cert.pem
    ```

## Заключение

Этот репозиторий предоставляет полные инструкции по генерации ключей и сертификатов, подписанию данных и проверке сертификатов с использованием OpenSSL. Инструкции включают команды для работы в командной строке и примеры программ на Python, обеспечивая надежную проверку сертификатов.
