# docker-redis
`docker-redis`

```sh
docker exec -it redis redis-cli -a secret
127.0.0.1:6379> KEYS cart:*
127.0.0.1:6379> GET cart:[user_id]
```
```
docker exec -it redis redis-cli -a secret
127.0.0.1:6379> FLUSHDB
```

# Access Redis CLI

## Connect to local Redis
`redis-cli`

## If Redis has a password (like in your settings)
`redis-cli -a your_password`

## Or connect and then authenticate
```sh
redis-cli
127.0.0.1:6379> AUTH tu_contraseña
```

# Useful commands for debugging your reservations

## Ver todas las keys (cuidado en producción)
`KEYS *`

## Search for specific reservation keys
`KEYS reserved:product:*`

## View the value of a specific key
`GET reserved:product:{productId}:{userId}`

## View key type
`TYPE reserved:product:...`

## View remaining lifespan (TTL)
`TTL reserved:product:...`

# To view your specific reservations

## Enter Redis CLI
`redis-cli`

## Search all reservations
`KEYS reserved:product:*`

## View a specific reservation (replaces the IDs)
`GET reserved:product:123e4567-e89b-12d3-a456-426614174000:user-456`

## View all keys with their values
`SCAN 0 MATCH reserved:product:* COUNT 100`

# Useful commands for cleaning

## Delete a specific key
`DEL reserved:product:...`

## Delete ALL reservations (careful!)
`DEL $(redis-cli KEYS "reserved:product:*")`

## Clean the entire database (CAUTION!)
`FLUSHDB`

## Exit Redis CLI
`exit`

# Practical example to verify your reservations:

## 1. Connect
`redis-cli`

## 2. View how many reservations there are
`DBSIZE`

## 3. View all booking keys
`KEYS reserved:*`

## 4. View a specific reservation
`GET reserved:product:product-id-123:user-id-456`

## 5. View TTL (if it expires)
`TTL reserved:product:product-id-123:user-id-456`
