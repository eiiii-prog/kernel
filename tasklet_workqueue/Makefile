obj-m = tasklet_ex1.o
obj-m = tasklet_ex2.o

all:
		make -C /lib/modules/$(shell uname -r)/build M=$(shell pwd) modules

clean:
		make -C /lib/modules/$(shell uname -r)/build M=$(shell pwd) clean
