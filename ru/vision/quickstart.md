# Как начать работать c [!KEYREF vision-short-name]

Этот раздел описывает, как начать использовать [!KEYREF vision-short-name] API для анализа изображений.

## Перед началом

1. Убедитесь, что у вас установлена утилита [cURL](https://curl.haxx.se), используемая в примерах.
1. [Получите идентификатор каталога](../resource-manager/operations/folder/get-id.md), на который у вас есть роль `editor` или выше. Идентификатор каталога используется для авторизации. Подробнее в разделе [Управление доступом](security/index.md).
1. Получите IAM-токен, необходимый для аутентификации в API ([о других способах аутентификации](api-ref/authentication.md)):

    ---

    **[!TAB CLI]**

    ```
    $ yc iam create-token
    ```

    **[!TAB API]**

    [!INCLUDE [create-iam-token-api-steps](../_includes/iam/create-iam-token-api-steps.md)]

    ---


## Проанализируйте изображение

Вы можете использовать любые возможности для анализа из [списка](concepts/index.md#features). Для примера, воспользуемся возможностью [Распознавание текста](concepts/ocr/index.md):

[!INCLUDE [text-detection-steps](../_includes/vision/text-detection-steps.md)]

#### Что дальше

* [Узнайте обо всех возможностях сервиса](concepts/index.md)
* [Найдите лица на фото](operations/face-detection/index.md)
* [Оцените качество изображения](operations/classification/quality.md)
* [Модерируйте изображения](operations/classification/moderation.md)
