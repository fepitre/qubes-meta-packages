SHELL = /bin/bash

ifneq (,$(wildcard /etc/fedora-release))
DIST = fc$(shell rpm --eval %{fedora})
else ifneq (,$(wildcard /etc/os-release))
DIST = $(shell grep VERSION_CODENAME= /etc/os-release | cut -d'=' -f2)
endif

ifeq (,$(DIST))
# On debian if previous attempt failed
# it means we are on sid
ifneq (,$(wildcard /etc/debian_version))
DIST = $(shell cut -d'/' -f1 /etc/debian_version)
endif
endif

DIST ?= fc42

install-dom0: install-fedora
	install -d $(DESTDIR)/etc/yum.repos.d
	install -m 0644 qubes-contrib-dom0-r4.2.repo.in $(DESTDIR)/etc/yum.repos.d/qubes-contrib-dom0-r4.2.repo
	sed -i "s/@DIST@/$(DIST)/g" $(DESTDIR)/etc/yum.repos.d/qubes-contrib-dom0-r4.2.repo

install-vm-debian:
	install -d $(DESTDIR)/etc/apt/sources.list.d
	sed "s/@DIST@/$(DIST)/" qubes-contrib-r4.2.list.in > $(DESTDIR)/etc/apt/sources.list.d/qubes-contrib-r4.2.list

install-vm-fedora: install-fedora
	install -d $(DESTDIR)/etc/yum.repos.d
	install -m 0644 qubes-contrib-vm-r4.2.repo-fedora $(DESTDIR)/etc/yum.repos.d/qubes-contrib-vm-r4.2.repo

install-vm-centos: install-centos
	install -d $(DESTDIR)/etc/yum.repos.d
	install -m 0644 qubes-contrib-vm-r4.2.repo-centos $(DESTDIR)/etc/yum.repos.d/qubes-contrib-vm-r4.2.repo
