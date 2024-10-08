# tetra-toolkit

Tools and documentation for TETRA decoding.

The installation instructions are given for Ubuntu 24.04.

## Install gnuradio and gr-osmosdr

```sh
sudo apt install git gnuradio gr-osmosdr
```

## Download the GRC file

```sh
git clone https://github.com/Tim---/tetra-toolkit
```

The GNU Radio Companion files are located in the `grc` folder.

First, you must build the TETRA Demod block : 

```sh
grcc grc/tetra_demod.grc
```

Next, open the file `grc/tetra_rx.grc` in GNU Radio Companion, and execute it.

## Using the GUI

On the "Coarse" tab, enter the "Center Frequency" of your Tetra downlink.
The channel should be located at offset 0 on the left plots.

You can use the "Channel" and "Constellation" tab to check that your signal is clean.

Use the controls on the right (fine freq, ppm, gain) to get a nice signal.

## Getting the bits

Once everything is good, the bits are sent by chunks over UDP to `127.0.0.1:1234`.
Now we need an application that actually interprets the bits.

# osmo-tetra

## Download and build osmo-tetra

```sh
sudo apt install git build-essential libosmocore-dev
git clone https://gitea.osmocom.org/tetra/osmo-tetra.git
cd osmo-tetra/src
make
```

## Execute tetra-rx

```sh
sudo apt install netcat-openbsd
mkdir /tmp/out
nc -l -u -p 1234 | ./tetra-rx -d /tmp/out /dev/stdin
```

You should see some output on the console.

Also, the decoded packets are sent over GSMTAP to 127.0.0.1:4729.
You can use Wireshark to see the packets:

```sh
sudo apt install wireshark
wireshark -k -i lo -f 'udp port 4729'
```
