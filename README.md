# XMage Server based on Alpine & OpenJDK

## Purpose
Builds a `mage-server` image based on the most recent version of the beta as defined by the `Download full BETA client` button on [xmage.today](http://xmage.today).

This project was created because the latest beta client won't work without the latest beta server, and I was unable to find any other published `Dockerfile`s that produced a suitable image.

The rest of this `README` comes from [LunarNightShade/docker-xmage-openjdk](https://github.com/LunarNightShade/docker-xmage-openjdk), from which this was forked, except I removed the example `docker-compose.yml` section and added a `docker-compose.yml` file instead.

---

## Usage
```
docker run -d -it \
	--name XMage \
	-p 17171:17171 \
	-p 17179:17179 \
	--add-host example.com:0.0.0.0 \
	-e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
	--restart unless-stopped \
	jshawdrums/docker-xmage-server-beta
```

XMage needs to know the domain name the server is running on. The `--add-host` option adds an entry to the containers `/etc/hosts` file for this domain. Replace `example.com` with your server IP address or domain name address.
Using the `XMAGE_*` environment variables you can modify the `config.xml` file.
You should always set `XMAGE_DOCKER_SERVER_ADDRESS` to the same value as your `--add-host` flag value.

---

## Available Environment Variables and Default Values

+ `JAVA_MIN_MEMORY=256M`
+ `JAVA_MAX_MEMORY=512M`
+ `XMAGE_DOCKER_SERVER_ADDRESS="0.0.0.0"`
+ `XMAGE_DOCKER_PORT="17171"`
+ `XMAGE_DOCKER_SECONDARY_BIND_PORT="17179"`
+ `XMAGE_DOCKER_MAX_SECONDS_IDLE="600"`
+ `XMAGE_DOCKER_AUTHENTICATION_ACTIVATED="false"`
+ `XMAGE_DOCKER_SERVER_NAME="mage-server"`
+ `XMAGE_DOCKER_ADMIN_PASSWORD="hunter2"`
+ `XMAGE_DOCKER_MAX_GAME_THREADS="10"`
+ `XMAGE_DOCKER_MIN_USERNAME_LENGTH="3"`
+ `XMAGE_DOCKER_MAX_USERNAME_LENGTH="14"`
+ `XMAGE_DOCKER_MIN_PASSWORD_LENGTH="8"`
+ `XMAGE_DOCKER_MAX_PASSWORD_LENGTH="100"`
+ `XMAGE_DOCKER_MAILGUN_API_KEY="X"`
+ `XMAGE_DOCKER_MAILGUN_DOMAIN="X"`

---

If you would like to preserve the database during updates and restarts you can mount a volume at `/xmage/mage-server/db`. (Important if you're using user authentication.)

Add `--mount source=xmage-db,target=/xmage/mage-server/db` to your `docker run` command.

---
