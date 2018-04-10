# Install Librdkafka
Before install the library **librdkafka** need to install __zlib__ and __openssl__ .
>__Note:__ also can use `--disable-lz4` and `--disable-ssl` when compile __librdkafka__
## Download File
```bash
#download zlib
wget https://zlib.net/zlib-1.2.11.tar.xz
tar xvf zlib-1.2.11.tar.xz
#download openssl
wget https://www.openssl.org/source/old/1.0.0/openssl-1.0.0s.tar.gz
tar xvf openssl-1.0.0s.tar.gz
#download librdkafka
git clone https://github.com/edenhill/librdkafka.git
```
##  Cross Compile
1. **zlib**
2. **openssl**
3. **librdkafk**
###  Zlib
```bash
cd zlib-1.2.11
./configure --prefix=/usr/local/zlib-arm 
```
#### Modify **Makefile**
Replace all `gcc` with `arm-linux-gnueabihf-gcc`
```bash
make
sudo make install
sudo cp -r /usr/local/zlib-arm/lib/* /usr/arm-linux-gnueabihf/lib
```
### Openssl
```bash
cd openssl-1.0.0s
./Configure --prefix=/usr/local/openssl-arm os/compiler:linux-armv4
make CC=arm-linux-gnueabihf-gcc CPP=arm-linux-gnueabihf-g++
sudo make install
sudo cp -r /usr/local/openssl-arm/lib/* /usr/arm-linux-gnueabihf/lib
```
### Librdkafka
```bash
cd librdkafka
./configure --prefix=/usr/local/librdkafka-arm --host=arm-linux-gnueabihf
make 
sudo make install 
```
##  Install
Can use `ldd` or `file` to validate `*.so` is for  ARM architecture before copy file.
```bash
#copy file to ARM
scp -r /usr/local/librdkafka-arm/lib/* /usr/local/zlib-arm/lib/* /usr/local/openssl-arm/lib/* user_name@arm_ip:/usr/lib
