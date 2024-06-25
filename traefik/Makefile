stack ?= traefik

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


backup-all:
	$(MAKE) backup-volume volume_name=plugins-storage
	$(MAKE) backup-volume volume_name=traefik-le


restore-all:
	$(MAKE) restore-volume volume_name=plugins-storage
	$(MAKE) restore-volume volume_name=traefik-le
