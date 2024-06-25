stack ?= media-stack

start:
	docker compose up -d --remove-orphans

start-all: start nginx-start

stop-all: nginx-stop stop

backup-volume:
	docker run --rm \
	--volume $(stack)_$(volume_name):/temp \
	--volume $(shell pwd):/backup \
	ubuntu \
	tar cvf /backup/backup-$(volume_name).tar /temp

restore-volume:
	docker run --rm \
	--volume $(stack)_$(volume_name):/temp \
	--volume $(shell pwd):/backup \
	ubuntu \
	tar xvf /backup/backup-$(volume_name).tar -C /temp --strip 1


update-all:
	docker compose pull
	docker compose up --force-recreate --build -d
	docker image prune -f


backup-all:
	$(MAKE) backup-volume volume_name=radarr-config
	$(MAKE) backup-volume volume_name=sonarr-config
	$(MAKE) backup-volume volume_name=prowlarr-config
	$(MAKE) backup-volume volume_name=jellyfin-config
	$(MAKE) backup-volume volume_name=qbittorrent-config
	$(MAKE) backup-volume volume_name=bazarr-config
	$(MAKE) backup-volume volume_name=heimdall-config
	$(MAKE) backup-volume volume_name=lidarr-config
	$(MAKE) backup-volume volume_name=readarr-config
	$(MAKE) backup-volume volume_name=mylar3-config
	$(MAKE) backup-volume volume_name=jellyseerr-config
	$(MAKE) backup-volume volume_name=dashy-userdata


restore-all:
	$(MAKE) restore-volume volume_name=radarr-config
	$(MAKE) restore-volume volume_name=sonarr-config
	$(MAKE) restore-volume volume_name=prowlarr-config
	$(MAKE) restore-volume volume_name=jellyfin-config
	$(MAKE) restore-volume volume_name=qbittorrent-config
	$(MAKE) restore-volume volume_name=bazarr-config
	$(MAKE) restore-volume volume_name=heimdall-config
	$(MAKE) restore-volume volume_name=lidarr-config
	$(MAKE) restore-volume volume_name=readarr-config
	$(MAKE) restore-volume volume_name=mylar3-config
	$(MAKE) restore-volume volume_name=jellyseerr-config
	$(MAKE) restore-volume volume_name=dashy-userdata



nginx-start:
	docker compose -f docker-compose-nginx.yml up -d

nginx-restart: nginx-stop nginx-start

nginx-stop:
	docker compose -f docker-compose-nginx.yml down

stop:
	docker compose down

restart: stop start

restart-all: stop-all start-all

nginx-logs:
	docker compose -f docker-compose-nginx.yml logs -f
