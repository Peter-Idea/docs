# Ключ

Ключ — это набор [версий](version.md), каждая из которых определяет алгоритм и криптографический материал для операций шифрования или расшифровки данных.
При создании ключа создается его первая версия, которая становится основной. Она по умолчанию используется в операциях с ключом, если во входных параметрах не указана другая версия.
При [ротации ключа](version.md#rotate-key) параметры новых версий наследуются от параметров ключа.

Основную версию ключа можно изменить в любой момент, указав произвольную старую версию. Для дополнительной безопасности ваших данных регулярно ротируйте ключи и используйте старые версии только для расшифровки данных. Это ограничит время использования криптографического материала.

## Параметры ключа {#parameters}

Для ключа {{ kms-short-name }} доступны следующие параметры:
* Идентификатор – уникальный идентификатор ключа в {{ yandex-cloud }}. Используется для работы с ключами с помощью SDK, API и CLI.
* Название — название ключа, неуникально и может быть использовано для работы с ключами с помощью CLI, если в каталоге только один ключ с таким названием.
* Алгоритм шифрования – алгоритм, используемый для шифрования в новых версиях ключа. Поддерживаются следующие алгоритмы симметричного шифрования в режиме [GCM](https://en.wikipedia.org/wiki/Galois/Counter_Mode): 
    * `AES_128` — алгоритм AES со 128-битными ключами.
    * `AES_192` — алгоритм AES с 192-битными ключами.
    * `AES_256` — алгоритм AES с 256-битными ключами.
* Период ротации — промежуток времени между автоматическими ротациями ключа.
* Статус — текущее состояние ключа. Возможные статусы: 
    * `Creating` — ключ создается.
    * `Active` — ключ может использоваться для шифрования и расшифровки.
    * `Inactive` — ключ не может использоваться.
    
    Статус ключа можно изменить с помощью метода [update](../api-ref/SymmetricKey/update).

## Использование ключа {#use}

Созданный ключ можно использовать в операциях шифрования и расшифровки данных при наличии определенных [ролей](../security/index.md#roles-list). Вы можете временно заблокировать операции с использованием ключа, отозвав роли или изменив его статус на `Inactive`. Подробнее читайте в разделе [{#T}](../security/index.md).

## Удаление ключа {#delete}

Удаление ключа или родительского ресурса (каталога или облака), в котором содержался ключ, приводит к уничтожению содержащегося в нем криптографического материала. После этого вы не сможете расшифровать данные, зашифрованные ключом.