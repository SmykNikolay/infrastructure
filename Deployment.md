# Сервисы AWS для развертывания веб-приложений

## Amazon S3 (Simple Storage Service)
- Сервис объектного хранения для хранения любых типов файлов
- Основные функции:
  - Высокая масштабируемость и надежность
  - Поддержка хостинга статических веб-сайтов
  - Возможность версионирования
  - Тонкая настройка доступа
  - Экономичные классы хранения

```bash
# Примеры команд S3
aws s3 mb s3://my-bucket-name  # Создать бакет
aws s3 cp ./build s3://my-bucket-name --recursive  # Загрузить файлы
```

## CloudFront
- Сервис Content Delivery Network (CDN)
- Преимущества:
  - Глобальная сеть точек присутствия
  - Низкая задержка доставки контента
  - Поддержка HTTPS с SSL/TLS
  - Интеграция с S3 и другими сервисами AWS
  - Защита от DDoS атак

```yaml
# Пример конфигурации CloudFront дистрибутива
Distribution:
  Origins:
    - DomainName: my-bucket.s3.amazonaws.com
      Id: S3Origin
  DefaultCacheBehavior:
    TargetOriginId: S3Origin
    ViewerProtocolPolicy: redirect-to-https
```

## AWS Amplify
- Платформа для разработки полного стека
- Функции:
  - Интеграция с CI/CD пайплайнами
  - Развертывание на основе веток
  - Настройка пользовательских доменов
  - Встроенный мониторинг
  - Аутентификация и авторизация

```yaml
# Пример amplify.yml
version: 1
frontend:
  phases:
    build:
      commands:
        - npm install
        - npm run build
  artifacts:
    baseDirectory: build
    files:
      - '**/*'
```

### Типичный процесс развертывания
1. Хранение статических файлов в S3
2. Настройка CloudFront для обслуживания из S3
3. Использование Amplify для автоматизированного развертывания
