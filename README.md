
NOTE: this is a thin wrapper of https://github.com/ysminnpu/IDEAir. You can check more details over there before you grab the code. 

# IDEAir

IDEAir is an open source IDE based on [cloud9](https://github.com/ajaxorg/cloud9).

IDEAir enables developers to write, build, debug, test their C/C++ applications all within a browser. The IDEAir server can be deployed on a remote or local machine. Especially, it can be deployed on an embedded system board such as Intel Edison board, and then developers can develop embedded applications over the air (WiFi). 

## Features

  * High performance ACE text editor with bundled syntax highlighting support
  * Support C/C++ applications build, debug, and run
  * Console shell to the server or board
  * Problem solving assistant with integrated StackOverflow knowledge
  * Project management

## Browser Support

We support the newer versions of Chrome, Firefox and Safari.

## Installation and Usage

Requirements:

  * NodeJS `0.10.x`

### Full IDEAir Installation

    mkdir IDEAir
    cd IDEAir
    wget https://raw.githubusercontent.com/ysminnpu/IDEAir-manifest/master/repo
    chmod +x ./repo 
    ./repo init -u https://github.com/ysminnpu/IDEAir-manifest.git
    ./repo sync
    cd cloud9
    npm install
    cd ../cloud9hub
    npm install

Start IDEAir server

    ./start-dev.sh

Use IDEAir

    Go to http://IDEAir_server:3105/#/dashboard with your favorite browser. 


### Full IDEAir Installation on the board
We use an embedded board such as Edison (32bit IA arch) as an example. And we suppose the board and the host share a same wlan network. The ip of board is 192.168.8.100. 

On host, install a version of 32bit node.js. In our experiment, we used http://nodejs.org/dist/v0.10.28/node-v0.10.28-linux-x86.tar.gz. Untar the package and include the bin directory in your PATH. Use "which node" to make sure you are using the node binary from that directory. 

Also make sure you are using 32bit CC, CXX from the Edison SDK. You can change them using "source /opt/poky-edison/1.5.1/environment-setup-i586-poky-linux". And verify your CC is from Edison SDK by "echo $CC".

Then follow the installation instruction mentioned above, to install a 32 bit version server on your host. This step helps us resolve all the package dependencies. 

Then create a tarball with tar cvzf IDEAir.tgz IDEAir. Copy it to the board with scp IDEAir.tgz root@192.168.8.100:/home. 

ssh root@192.168.8.100; cd /home/; tar xzvf IDEAir.tgz; cd IDEAir/cloud9hub/. Change config.js to use a proper url for the board - our test uses 192.168.8.100. 

Start server with npm start. 

On the host, google-chrome 192.168.8.100/#/dashboard. 


### Only Install cloud9 (no project management feature)

    git clone https://github.com/ysminnpu/IDEAir.git cloud9
    cd cloud9
    npm install

The above install steps create a `cloud9` directory with a `bin/cloud9.sh`
script that can be used to start Cloud9:

    bin/cloud9.sh

Optionally, you may specify the directory you'd like to edit:

    bin/cloud9.sh -w ~/git/myproject

Cloud9 will be started as a web server on port `-p 3131`, you can access it by
pointing your browser to: [http://localhost:3131](http://localhost:3131)

By default Cloud9 will only listen to localhost.
To listen to a different IP or hostname, use the `-l HOSTNAME` flag.
If you want to listen to all IP's:

    bin/cloud9.sh -l 0.0.0.0

If you are listening to all IPs it is adviced to add authentication to the IDE.
You can either do this by adding a reverse proxy in front of Cloud9,
or use the built in basic authentication through the `--username` and `--password` flags.

    bin/cloud9.sh --username leuser --password c9isawesome

Cloud9 is compatible with all connect authentication layers,
to implement your own, please see the `plugins-server/cloud9.connect.basic-auth` plugin
on how we added basic authentication.

For a quick trial, IDEAir can be started as follows. 

    npm start

It is the same as 

    ./bin/cloud9.sh -w testcases/c/testMakefile -l 0.0.0.0

As you will see, a test C project will be opened. 

## License

The GPL version 3, read it at [http://www.gnu.org/licenses/gpl.txt](http://www.gnu.org/licenses/gpl.txt)

## Contact
[Shoumeng Yan](mailto:shoumeng.yan@gmail.com)
