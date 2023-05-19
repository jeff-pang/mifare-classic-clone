# mifare-classic-clone
Instructions on how to clone mifare classic 1k cards

This instruction give a brief description on how to clone mifare classic using libnfc and external usb nfc card reader `ACR122U` on MacOS (Ventura on M1 silicon as of this writing, but I have done this before for intel chip in older MacOS)

## Preparation

You need to self compile `libnfc` and `mfoc` but the dependencies can be installed via homebrew 

compile and install `libnfc`

```
brew install `libusb`

git clone https://github.com/nfc-tools/libnfc.git
cd libnfc
autoreconf -iv
./configure --with-drivers=acr122_pcsc
make && make install
```

compile and install `mfoc`

```
git clone https://github.com/nfc-tools/mfoc.git
cd mfoc
autoreconf -is
./configure
make && make install
```

*replace make install with sudo make install if necessary (e.g make && sudo make install)

## Clone

Make sure you have blank writable mifare classic cards also knowns as chinese magic cards or magic cards

Dump a copy of the original card you want to clone using the following command

`mfoc -P 500 -O original.dmp`

then dump a copy of your magic card

`mfoc -P 500 -O blank.dmp`

then place your magic card on the nfc reader and the following command will write to the magic card. Note that the command is case sensitive

`nfc-mfclassic W a original.dmp blank.dmp` 

or

`nfc-mfclassic W b original.dmp blank.dmp` 
