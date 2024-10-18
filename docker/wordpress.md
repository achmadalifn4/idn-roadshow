build directory
```
mkdir web
```
Create docker-compose.yml
```
nano docker-compose.yml

services:

  wordpress:
    image: wordpress
    container_name: wordpress
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    networks:
      wpnetworks:
        ipv4_address: 172.18.0.2
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:8.0
    container_name: db
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_ROOT_PASSWORD: examplepass
    networks:
      wpnetworks:
        ipv4_address: 172.18.0.3
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:

networks:
  wpnetworks:
    driver: bridge
    ipam:
      config:
        - subnet: 172.18.0.0/24
          gateway: 172.18.0.1
```
Edit konfigurasi wordpress
```
docker exec -it wordpress /bin/bash
cat << EOF >> .htaccess
php_value upload_max_filesize 100M
php_value post_max_size 100M
php_value max_execution_time 300
php_value max_input_time 300
EOF
```
