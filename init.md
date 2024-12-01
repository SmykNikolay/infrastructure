# Инструкция по развертыванию React-приложения на VPS


## Настройка стенда
Количество серверов = (Общее количество запросов в секунду) / (Обрабатываемые запросы одним сервером)
1 сервер = 250 запросов в секунду (надо смотреть на загрузку до 75%)

5000 пользователей / 5 секунд = 1000 запросов/сек.
1000 / 250 = 4 сервера.

-----------

Вариант с CDN (AWS CloudFront)
S3 + CloudFront или AWS Amplify.
С настройкой CI/CD (#.gitlab-ci.yml)

## Linting и форматирование
- ESLint
- Prettier
- Husky
- Lint-staged
- nvmrc
- StyleLint

```yaml
stages:
  - lint
  - test
  - build
  - security
  - performance
  - deploy
  - monitoring

lint:
  stage: lint
  script:
    - npm run lint
    - npm run prettier:check

test:
  stage: test
  script:
    - npm run test
    - npm run test:e2e
    - npm run test:coverage

security:
  stage: security
  script:
    - npm audit
    - npm run security-scan
    - npm run dependency-check

performance:
  stage: performance
  script:
    - npm run lighthouse
    - npm run bundle-analyzer

deploy:
  stage: deploy
  script:
    - npm run build
    - aws s3 sync dist/ s3://bucket-name
    - aws cloudfront create-invalidation

monitoring:
  stage: monitoring
  script:
    - npm run health-check
    - npm run error-tracking
```



## 5. Безопасность
- [ ] Настроить CORS
- [ ] Внедрить rate limiting
- [ ] Настроить безопасные заголовки HTTP
- [ ] Регулярное обновление зависимостей
- [ ] Настроить логирование

## 6. Оптимизация
- [ ] Настроить code splitting
- [ ] Оптимизировать сборку
- [ ] Настроить кэширование
- [ ] Оптимизировать изображения
- [ ] Настроить CDN