Installation
------------------

* Mandatory requirements: 
  * Common:
    * cmake              https://cmake.org/
    * libfftw            http://www.fftw.org/
    * PolarSSL/mbedTLS   https://tls.mbed.org
  * srsUE:
    * Boost:             http://www.boost.org
  * srsENB:
    * Boost:             http://www.boost.org
    * lksctp:            http://lksctp.sourceforge.net/
    * config:            http://www.hyperrealm.com/libconfig/
  * srsEPC:
    * Boost:             http://www.boost.org
    * lksctp:            http://lksctp.sourceforge.net/
    * config:            http://www.hyperrealm.com/libconfig/

For example, on Ubuntu, one can install the mandatory build dependencies with:
```
sudo apt-get install cmake libfftw3-dev libmbedtls-dev libboost-program-options-dev libconfig++-dev libsctp-dev
```
or on Fedora:
```
dnf install cmake fftw3-devel mbedtls-devel lksctp-tools-devel libconfig-devel boost-devel
```
For CentOS, use the Fedora packages but replace `libconfig-devel` with just `libconfig`.

Note that depending on your flavor and version of Linux, the actual package names may be different.

* Optional requirements: 
  * srsgui:              https://github.com/srslte/srsgui - for real-time plotting.
  * libpcsclite-dev:     https://pcsclite.apdu.fr/ - for accessing smart card readers

* RF front-end driver:
  * UHD:                 https://github.com/EttusResearch/uhd
  * SoapySDR:            https://github.com/pothosware/SoapySDR
  * BladeRF:             https://github.com/Nuand/bladeRF
  * ZeroMQ:              https://github.com/zeromq

Download and build srsLTE: 
```
cd srsLTE
mkdir build
cd build
cmake ../
make
make test
```

Install srsLTE:

```
sudo make install
srslte_install_configs.sh user
```

This installs srsLTE and also copies the default srsLTE config files to
the user's home directory (~/.config/srslte).

Equipment Required
------------------

* [USRP B210](https://www.ettus.com/all-products/ub210-kit/)
* [QCSuper](https://github.com/P1sec/QCSuper)
* Android Device supported by QCSuper

Edits before conducting attacks
------------------

**IMSI Catching**
In `s1ap_nas_transport.cc` : If commented, uncomment lines 156 to 168.
In `nas.cc`: uncomment lines 130-139. Comment other edited lines.

**Attach Reject**
In `s1ap_nas_transport.cc` : If uncommented, comment lines 156 to 168.
In `nas.cc`: uncomment lines 99-113. Comment other edited lines.

**Authentication Failure**
In `s1ap_nas_transport.cc` : If uncommented, comment lines 156 to 168.
In `nas.cc`: uncomment lines 116-127. Comment other edited lines.

Running the attacks
--------------------

Make sure to setup the USRP B210 prior to running the attacks.

In terminal 1:
```
sudo srsepc
```

In terminal 2:
```
sudo srsenb
```

Connect Android phone to the PC and run QCSuper. Monitor Wireshark for incoming and outgoing packets.

Note: If the attacks don't seem to be working, try finding the rogue eNB manually on the phone and try connecting.

