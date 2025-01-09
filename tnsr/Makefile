VENDOR=NetGate
NAME=TNSR
IMAGE_FORMAT=qcow2
IMAGE_GLOB=*.qcow2

# match versions like:
# TNSR-23.11-3.qcow2
VERSION=$(shell echo $(IMAGE) | sed -e 's/\TNSR-\(.*\).qcow2/\1/')


-include ../makefile-sanity.include
-include ../makefile.include

build:
	$(MAKE) docker-image
