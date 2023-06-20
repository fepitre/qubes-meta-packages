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

install-vm-debian:
	install -d $(DESTDIR)/etc/apt/trusted.gpg.d
	gpg --dearmor --output \
		$(DESTDIR)/etc/apt/trusted.gpg.d/qubes-4-contrib-debian-keyring.gpg \
		qubesos-contrib-release-4-debian.asc

install-vm-fedora: install-fedora

install-vm-centos: install-centos

install-fedora:
	install -d $(DESTDIR)/etc/pki/rpm-gpg/
	install -m 0644 qubesos-contrib-release-4-fedora.asc \
		$(DESTDIR)/etc/pki/rpm-gpg/RPM-GPG-KEY-qubes-4-contrib-fedora
	ln -s RPM-GPG-KEY-qubes-4-contrib-fedora \
		$(DESTDIR)/etc/pki/rpm-gpg/RPM-GPG-KEY-qubes-4.2-contrib-fedora
install-centos:
	install -d $(DESTDIR)/etc/pki/rpm-gpg/
	install -m 0644 qubesos-contrib-release-4-centos.asc \
		$(DESTDIR)/etc/pki/rpm-gpg/RPM-GPG-KEY-qubes-4-contrib-centos
	ln -s RPM-GPG-KEY-qubes-4-contrib-centos \
		$(DESTDIR)/etc/pki/rpm-gpg/RPM-GPG-KEY-qubes-4.2-contrib-centos
