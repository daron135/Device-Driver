APP := ledkey_app_cys
MOD := ledkey_dev_cys
SRC := $(APP).o
obj-m := $(MOD).o

CROSS = ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
CC := arm-linux-gnueabihf-gcc
KDIR := "User Directory Address"/kernel/linux
PWD := $(shell pwd)


default:$(APP)
	$(MAKE) -C $(KDIR) M=$(PWD) modules $(CROSS)
	cp $(MOD).ko /srv/nfs
$(APP):$(SRC)
	$(CC) $(APP).c -o $(APP)
	cp $(APP) /srv/nfs
clean:
	rm -rf *.ko
	rm -rf *.mod.*
	rm -rf .*.cmd
	rm -rf *.o
	rm -rf modules.order
	rm -rf Module.symvers
	rm -rf $(MOD).mod
	rm -rf .tmp_versions
	rm -rf $(APP)
