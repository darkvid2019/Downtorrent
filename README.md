bit-torrent
===========

DownTorrent client built with Python's asyncio

Features
--------

* Downloading torrents and sharing received data
* Graphical interface (supports Drag'n'Drop and can be assigned to *.torrent files in system "Open with..." dialog)
* Console interface
* Pausing torrents, watching progress, download and upload speed, ETA
* Selecting which files in a torrent you want to download
* Saving state between program restarts

Architecture
------------

In this project, I tried to avoid threads and use only asynchronous I/O. As a result, all algorithms and network interaction work in one thread running an asyncio event loop, but there are still a few additional threads:

* Non-blocking disk I/O [isn't supported][asyncio-fs] by asyncio. To prevent freezes for up to a second
during disk writing, blocking I/O runs in a [ThreadPoolExecutor][].
* PyQt GUI runs in the main thread and invokes an asyncio event loop in a separate [QThread][]. Another option is
to use a Qt event loop in asyncio with [quamash][], but this increases UI reaction time, and the Qt event loop
may be less efficient than asyncio's default one.

Installation
------------

The program requires Python 3.5+ and works on Linux, macOS, and Windows. You also need PyQt 5 to run GUI.

On Ubuntu 16.04 or newer, run:

```bash
sudo apt-get install python3-pip python3-pyqt5
git clone https://github.com/darkvid2019/Downtorrent.git && cd Downtorrent
sudo python3 -m pip install -r requirements.txt
```

On macOS, run:

```bash
python3 -m pip install PyQt5
git clone https://github.com/darkvid2019/Downtorrent.git && cd bit-torrent
python3 -m pip install -r requirements.txt
```

Usage
-----

### Graphical interface

Run:

    python3 downtorrent.py

Author
------

Copyright &copy; 2021 joel broutin
