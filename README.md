

# Installation Guide: Deploying Cacti with MariaDB 🌐

### Step 1: Deploying MariaDB in Your Server
To kickstart the process, you need to deploy MariaDB in your server environment. Here's a sample `stack-deploy.yml` file you can use:

```yaml
# Docker pull https://github.com/million12/docker-mariadb
# Docker pull https://hub.docker.com/r/polinux/cacti

# MariaDB Stack YAML:
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
```

### Step 2: Deploying Cacti with MariaDB Integration
Once MariaDB is deployed and you've created a new database and user passwords, you can proceed with deploying Cacti using the following stack YAML configuration:

```yaml
# Cacti Stack YAML:

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

```

### Enhancements and Tips:
- Ensure that MariaDB is properly configured with the required user permissions and access controls before integrating it with Cacti.
- Consider adding environment variables and configurations to the Cacti stack YAML file to customize the deployment according to your requirements.
- Monitor the interactions between Cacti and MariaDB to ensure seamless operation and data management within the Cacti monitoring platform.

This guide aims to assist you in setting up a robust monitoring environment with Cacti and MariaDB. Feel free to reach out for any further assistance or clarification on the deployment process. Happy monitoring! 🚀
