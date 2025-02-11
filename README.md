#### -- Notes from me --

The story behind the code here, started with a label printer Brother QL-570 that I own.
Unfortunately it is little old and does not have some extras of the modern label printers as a web design and printing of the labels.
In addition its label printing software is only for Windows.

Going to the computer, where the printer is attahced or switching of OS-es only to print labels, for me looks not so comfortable.

So I searched around for ideas and I found the project “pklaus/brother_ql_web”.
It represents a web functionality that allows printing of labels from a web browser.

The project is ideal to be deployed on something small like Raspberry Pi.

So I forked the project and I made little extension* of its functionality and minor bug fixes*.

Then I evaluated where it is the best to deploy it. I needed a microcomputer that is not so extended like Raspberry Pi (with HDMI, LAN and so on), but to have its own Wifi.
Luckly I have few [C.H.I.P.](https://en.wikipedia.org/wiki/CHIP_(computer)) (a $9 computer from Next Thing Co., launched via a successful Kickstarter campaign).

On it I deployed all the necessary software, needed for the functionality of the forked “brother_ql_web” project.

As a result I have a label printer that is connected to the home Wifi network and on it I can print labels from desktop or mobile web browser.

I share the idea for anyone that has the same label printer's family (Brother QL) and wants to redo the same, so here it is.


**Remarks:**

Added functionality:
*- Originally the text can be aligned at left, right or at center, but the whole text segment is printed centered to the label. It has been added possability to align the text segment at left, right or at center (respectively when the label is rotatated the directions are top, bottom and middle).*

Bugfixing:
*- When the page is loaded for the first time, both checkboxes of label orientation are unchecked.*

Configuration notes: 
*- It is important the exact printer model to be filled in the config file, because not all of the functionalities are present in the different models.*


#### -- The notes of the original project are bellow --



## brother\_ql\_web

This is a web service to print labels on Brother QL label printers.

You need Python 3 for this software to work.

![Screenshot](./static/images/screenshots/Label-Designer_Desktop.png)

The web interface is [responsive](https://en.wikipedia.org/wiki/Responsive_web_design).
There's also a screenshot showing [how it looks on a smartphone](./static/images/screenshots/Label-Designer_Phone.png)

### Installation

**ProTip™**: If you know how to use Docker, you might want to use my ready-to-use Docker image to deploy this software.
It can be found [on the Docker hub](https://hub.docker.com/r/pklaus/brother_ql_web/).  
Otherwise, follow the instructions below.

Get the code:

    git clone https://github.com/pklaus/brother_ql_web.git

or download [the ZIP file](https://github.com/pklaus/brother_ql_web/archive/master.zip) and unpack it.

Install the requirements:

    pip install -r requirements.txt

In addition, `fontconfig` should be installed on your system. It's used to identify and
inspect fonts on your machine. This package is pre-installed on many Linux distributions.
If you're using a Mac, I recommend to use [Homebrew](https://brew.sh) to install
fontconfig using [`brew install fontconfig`](http://brewformulas.org/Fontconfig).

### Configuration file

Copy `config.example.json` to `config.json` (e.g. `cp config.example.json config.json`) and adjust the values to match your needs.

### Startup

To start the server, run `./brother_ql_web.py`. The command line parameters overwrite the values configured in `config.json`. Here's its command line interface:

    usage: brother_ql_web.py [-h] [--port PORT] [--loglevel LOGLEVEL]
                             [--font-folder FONT_FOLDER]
                             [--default-label-size DEFAULT_LABEL_SIZE]
                             [--default-orientation {standard,rotated}]
                             [--model {QL-500,QL-550,QL-560,QL-570,QL-580N,QL-650TD,QL-700,QL-710W,QL-720NW,QL-1050,QL-1060N}]
                             [printer]
    
    This is a web service to print labels on Brother QL label printers.
    
    positional arguments:
      printer               String descriptor for the printer to use (like
                            tcp://192.168.0.23:9100 or file:///dev/usb/lp0)
    
    optional arguments:
      -h, --help            show this help message and exit
      --port PORT
      --loglevel LOGLEVEL
      --font-folder FONT_FOLDER
                            folder for additional .ttf/.otf fonts
      --default-label-size DEFAULT_LABEL_SIZE
                            Label size inserted in your printer. Defaults to 62.
      --default-orientation {standard,rotated}
                            Label orientation, defaults to "standard". To turn
                            your text by 90°, state "rotated".
      --model {QL-500,QL-550,QL-560,QL-570,QL-580N,QL-650TD,QL-700,QL-710W,QL-720NW,QL-1050,QL-1060N}
                            The model of your printer (default: QL-500)

### Usage

Once it's running, access the web interface by opening the page with your browser.
If you run it on your local machine, go to <http://localhost:8013> (You can change
the default port 8013 using the --port argument).
You will then be forwarded by default to the interactive web gui located at `/labeldesigner`.

All in all, the web server offers:

* a Web GUI allowing you to print your labels at `/labeldesigner`,
* an API at `/api/print/text?text=Your_Text&font_size=100&font_family=Minion%20Pro%20(%20Semibold%20)`
  to print a label containing 'Your Text' with the specified font properties.

### License

This software is published under the terms of the GPLv3, see the LICENSE file in the repository.

Parts of this package are redistributed software products from 3rd parties. They are subject to different licenses:

* [Bootstrap](https://github.com/twbs/bootstrap), MIT License
* [Glyphicons](https://getbootstrap.com/docs/3.3/components/#glyphicons), MIT License (as part of Bootstrap 3.3)
* [jQuery](https://github.com/jquery/jquery), MIT License
