# Варианты балансировки нагрузки в NGINX

## Настройка через nGinx

```file 
nginx.conf
```

```conf
 least_conn;  # Метод балансировки по наименьшему количеству соединений
    server frontend1:80 weight=3;
    server frontend2:80 weight=2;
    server frontend3:80 backup;  # Резервный сервер 
```
Отказоустойчивость (есть backup сервер)
Балансировка нагрузки по наименьшему количеству соединений
Взвешенное распределение трафика

-----------------------

### 1. Round Robin (по умолчанию)
```nginx
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}
```
- Простое поочередное распределение запросов
- Подходит для серверов с одинаковой производительностью

### 2. IP Hash
```nginx
upstream backend {
    ip_hash;
    server backend1.example.com;
    server backend2.example.com;
}
```
- Распределение на основе IP-адреса клиента
- Обеспечивает привязку клиента к серверу (session persistence)

### 3. Weighted Round Robin
```nginx
upstream backend {
    server backend1.example.com weight=5;
    server backend2.example.com weight=1;
}
```
- Распределение с учетом весов серверов
- Полезно при разной мощности серверов

### 4. Fair
```nginx
upstream backend {
    fair;
    server backend1.example.com;
    server backend2.example.com;
}
```
- Распределение по времени ответа
- Требует дополнительный модуль nginx-upstream-fair

### 5. Generic Hash
```nginx
upstream backend {
    hash $request_uri consistent;
    server backend1.example.com;
    server backend2.example.com;
}
```
- Распределение на основе произвольного ключа
- Поддерживает consistent hashing

### 6. Random
```nginx
upstream backend {
    random two;
    server backend1.example.com;
    server backend2.example.com;
}
```
- Случайное распределение
- Опция "two" выбирает случайным образом из двух серверов

### Дополнительные параметры серверов

```nginx
upstream backend {
    server backend1.example.com max_fails=3 fail_timeout=30s;
    server backend2.example.com max_conns=1000;
    server backend3.example.com slow_start=30s;
    server backend4.example.com down;
}
```

- `max_fails` - максимальное количество неудачных попыток
- `fail_timeout` - время ожидания после неудачных попыток
- `max_conns` - максимальное количество соединений
- `slow_start` - постепенное увеличение нагрузки
- `down` - отключение сервера из ротации