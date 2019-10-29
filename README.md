# electron-serialport-poc

This test assumes you have a prolific USB to RS-232 Serial Adapter.

## Performing Loopback Test

### Dependencies

- First you must install the [prolific driver](https://plugable.com/drivers/prolific) for your Operating System. 
- After installing and restarting your system, you must next identify the port for testing. For example, on Mac you can run `ls /dev | grep tty.usb` which should return `tty.usbserial`, if your driver was installed correctly.
- Next, install `@serialport/repl` by running `npm install -g @serialport/repl`
- *The TXD(3) pin must be connected to the RXD(2) pin. - [DE-9 Male diagram](https://user-images.githubusercontent.com/1910114/67594606-b6def000-f732-11e9-9a4d-28951fb50c8f.png)*

### Performing Test

- Now let's perform the test in the serialport repl!

```sh
serialport-repl {path-to-port} # serialport-repl /dev/tty.usbserial on a Mac
# This will pre-load a `port` variable with a connection to the serial adapter.
> port.open() # Allow the port to accept I/O
> port.write("Hello World!")
> const output = port.read() 
<Buffer 48 65 6c 6c 6f 20 77 6f 72 6c 64 21> # If connection between pins was successfully made
> output.toString(); # should be "Hello World!"
```

### Documentation

- [How to Do a Serial Loopback Test](http://www.ni.com/tutorial/3450/en/)
- [SerialPort Docs](https://serialport.io/docs/guide-about)

## Electron App

To clone and run this repository you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# git clone the repository and run the following
cd electron-serialport-poc
# Install dependencies
npm install
# Run the app
npm start
```

This will start an electron app which will list out any serial connections which the serialport library can discover.
