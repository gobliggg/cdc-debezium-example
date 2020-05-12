# CDC Debezium Example
CDC Debezium example based on Docker.

## Getting Started

### Prerequisites
```
> [Git](https://git-scm.com/downloads)
> [Docker](https://www.docker.com/products/docker) >= 17.12
```

### Installing
1. Clone this repository anywhere on your machine:
```
git clone git@github.com:imansuparman/cdc-debezium-example.git
```

2. Run docker compose build
```
docker-compose up -d --build
```

### Usage
1. Register a connector to monitor the database
```
curl --request POST \
  --url http://127.0.0.1:8083/connectors \
  --header 'content-type: application/json' \
  --data '{
	"name": "inventory-connector",
	"config": {
		"connector.class": "io.debezium.connector.mysql.MySqlConnector",
		"tasks.max": "1",
		"database.hostname": "mysql",
		"database.port": "3306",
		"database.user": "root",
		"database.password": "secret",
		"database.server.id": "184054",
		"database.server.name": "dbserver1",
		"database.whitelist": "inventory",
		"database.history.kafka.bootstrap.servers": "kafka:9092",
		"database.history.kafka.topic": "dbhistory.inventory"
	}
}'
```

2. Display list of connectors
```
curl --request GET \
  --url http://127.0.0.1:8083/connectors
```

3. Get a connector by name
```
curl --request GET \
  --url http://127.0.0.1:8083/connectors/inventory-connector
```

4. Get a list of topics

```
docker-compose run --rm kafka list-topics
```

5. Watch topic by topic name
```
docker-compose run --rm kafka watch-topic -a -k `topic name`
```

## Contributing
1. Fork it (<https://github.com/yourname/yourproject/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


## Authors
TBS

## Acknowledgments
- [Debezium - Getting Started Tutorial](https://debezium.io/documentation/reference/tutorial.html)