# LocalEnv
## Порядок разворачивания
* docker-compose up -d
* cd ./nginx/certs
* openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
* echo '172.43.1.100 app.loc www.app.loc' | sudo tee -a /etc/hosts

## После разворачивания
* https://app.loc/ - адрес приложения
## Нюансы
* IP и прочее в .env
* xdebug шторм сам подцепит, надо только расширение поставить. Я использую Xdebug-ext (Firefox)
