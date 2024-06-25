stack ?= paperless

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
	$(MAKE) backup-volume volume_name=data
	$(MAKE) backup-volume volume_name=pgdata
	$(MAKE) backup-volume volume_name=redisdata


restore-all:
	$(MAKE) restore-volume volume_name=data
	$(MAKE) restore-volume volume_name=pgdata
	$(MAKE) restore-volume volume_name=redisdata
