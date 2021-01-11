## Zend_oo and Sidechains-SDK build

### 1. Zend_oo
I got dependencies with
```
$ sudo apt-get install \
      build-essential pkg-config libc6-dev m4 g++-multilib \
      autoconf libtool ncurses-dev unzip git python \
      zlib1g-dev bsdmainutils automake curl
```
I moved to `Desktop` and:
```
$ git clone https://github.com/HorizenOfficial/zend_oo.git && cd zend_oo
# Build
$ ./zcutil/build.sh -j$(nproc)
# fetch key
$ ./zcutil/fetch-params.sh
# Run
$ ./src/zend -regtest -websocket
```
