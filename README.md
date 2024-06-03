# Installition Cacti with MariaDb
### Firstly you should deploy mariadb in your server 
Sample stack-deploy.yml
### Docker pull https://github.com/million12/docker-mariadb
### Docker pull https://hub.docker.com/r/polinux/cacti

### Mariadb Stack yml :

#### 
    image: million12/mariadb:latest
    ports:
      - "3306:3306"

    restart: always
    environment:
      MARIADB_PASS: DBPASS

    volumes:
      #- /etc/mysql/mariadb.conf.d/50-server.cnf:/etc/mysql/mariadb.conf.d/50-server.cnf
      #- /var/log/mysql:/var/log/mysql
      #- /etc/my.cnf.d/:/etc/my.cnf.d/
      - /var/lib/mysql:/var/lib/mysql
    networks:
      - cacti_network
    networks:
      cacti_network:
      external: true


## Cacti Stack yml

###

    image: polinux/cacti:latest
    ports:
      - "80:80"
    environment:
      - TIMEZONE=Asia/Tehran
      - DB_USER=DBUSER
      - DB_PASS=DBPASS
      - DB_ADDRESS=mariadb
    depends_on:
      - mariadb
    networks:
      - cacti_network

     networks:
       cacti_network:
       external: true
