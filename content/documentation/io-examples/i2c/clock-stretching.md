---
title: I²C Clock Stretching
weight: 231
tags: ["I2C"]
---

## Clock Stretching

{{% notice warning %}}Please be aware there are some hardware issues when using
the Raspberry Pi with devices that expect to be able to use clock stretching,
for more info see
["Adventures in I2C: clock stretching on the Raspberry Pi"](https://www.recantha.co.uk/blog/?p=19880)
and ["I2C stretch bug. Been fixed or not?"](https://www.raspberrypi.org/forums/viewtopic.php?t=220428).{{%
/notice %}}

[Clock stretching](https://en.wikipedia.org/wiki/I%C2%B2C#Clock_stretching_using_SCL)
in I2C allows a slave device to halt the master before a more data is sent. This
is often the case when the slave device writes to an EEPROM etc. which takes
longer than a usual read or write to a register.

On the Raspberry Pi clock stretching can be configured by using a higher timeout
while waiting for a slave to respond. This is something that can not be done by
the pi4j, as it requires root privileges.

There are two ways to change the `clkt_tout` value.
This [repository path](https://github.com/raspihats/raspihats/tree/master/clk_stretch) has
two files, a `i2c1_get_clkt_tout.c` and `i2c1_set_clkt_tout.c`. Build them as follows:

**Prepare:**

```shell
# install gcc to compile the c files
apt install build-essential

mkdir clkt_tout
cd clkt_tout/
wget wget https://raw.githubusercontent.com/raspihats/raspihats/master/clk_stretch/i2c1_get_clkt_tout.c
wget wget https://raw.githubusercontent.com/raspihats/raspihats/master/clk_stretch/i2c1_set_clkt_tout.c

```

**Makefile**

Save as `Makefile`

```makefile
CC=gcc
CFLAGS=-Wall

.PHONY: all install uninstall clean

all: i2c1_set_clkt_tout i2c1_get_clkt_tout

i2c_get_clkt_tout: i2c1_get_clkt_tout.c
        $(CC) -o i2c1_get_clkt_tout i2c1_get_clkt_tout.c

i2c_set_clkt_tout: i2c1_set_clkt_tout.c
        $(CC) -o i2c1_set_clkt_tout i2c1_set_clkt_tout.c

install:
        cp i2c1_get_clkt_tout /usr/local/bin/i2c1_get_clkt_tout
        cp i2c1_set_clkt_tout /usr/local/bin/i2c1_set_clkt_tout

uninstall:
        rm -f /usr/local/bin/i2c1_get_clkt_tout
        rm -f /usr/local/bin/i2c1_set_clkt_tout

clean:
        rm -f i2c1_set_clkt_tout i2c1_get_clkt_tout

```

**Build and install**

```shell
make
sudo make install
```

**Usage**

```shell
# read current clkt_tout:
$ sudo i2c1_get_clkt_tout 
i2c1_get_clkt_tout: CLKT.TOUT = 1000

# set timeout to 1 second:
i2c_set_clkt_tout 1000
```