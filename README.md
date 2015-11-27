# tetra-toolkit
Tools and documentation for TETRA decoding.

The installation instructions are given for Ubuntu 15.10.

## Install gnuradio and libosmosdr

```
sudo apt-get install gnuradio libosmosdr0 osmo-sdr gr-osmosdr
```

## Install the library for your device

Depending on your device, you have to install a different library (see http://sdr.osmocom.org/trac/wiki/GrOsmoSDR).

If you have a RTL-SDR dongle, use :
```
sudo apt-get install rtl-sdr librtlsdr0
```

## Download the GRC file

The GNU Radio Companion files are located in the `grc` folder.

First, you must build the TETRA Demod block : 

```
grcc grc/tetra_demod.grc
```

Next, open the file `grc/tetra_rx.grc` in GNU Radio Companion, and execute it.

