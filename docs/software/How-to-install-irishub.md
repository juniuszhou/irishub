# How to install `iris` 

### The Latest version of IRIShub : v0.13.1
refer to : https://github.com/irisnet/irishub/releases/latest
```
Please replace <latest_iris_version> with v0.13.1 while using "git checkout" 
```

You can download the source code from github and compile it locally.

#### Configure Your Server

It's recommended that you run a validator node on Linux Server.

**Recommended Configurations:**

1. 2 CPU
2. Memory: 6GB
3. Disk: 256GB SSD
4. OS: Ubuntu 16.04 LTS
5. Bandwidth: 20Mbps
6. Allow all incoming connections on TCP port 26656 and 26657

#### Compile Source Code

- Install Go 1.10+

```
$ sudo add-apt-repository ppa:gophers/archive
$ sudo apt-get update
$ sudo apt-get install golang-1.10-go
```

> Note that golang-1.10-go puts binaries in /usr/lib/go-1.10/bin. If you want them on your PATH, you need to make that change yourself.

Using snaps also works quite well:

```
This will give you the latest version of go
$ sudo snap install --classic go
```

> A restart is required for the command to be recognized.

Then you need to verify the versions of Go:

```
$ go version
go version go1.10.3 darwin/amd64
```

Then, you need to add `GOPATH` to system `PATH` , then your system could correctly compile the code.

Open your `.profile` in your home directory. Add the following lines at the end of file:

```
GOPATH=$HOME/go
PATH=$GOPATH/bin:$PATH
```

Save the file and exit the editor. Then run the following to make your bash reload your profile configurations.

```
$ source $HOME/.profile
```

Now you should see something like this if you echo your\$GOPATH and \$PATH variables

```
$ echo $GOPATH
/home/iris/go
$ echo $PATH
/home/isir/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

- Get the code and compile Iris

After setting up Go correctly, you should be able to compile and run `iris`.
Make sure that your server can access to google.com because our project depends on some libraries provided by google.

* To compile for `testnet`:
Please checkout the latest version，refer to：https://github.com/irisnet/irishub/releases/latest
```
mkdir -p $GOPATH/src/github.com/irisnet
cd $GOPATH/src/github.com/irisnet
git clone https://github.com/irisnet/irishub
cd irishub && git checkout <latest_iris_version>
curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
make get_tools
make get_vendor_deps
source scripts/setTestEnv.sh
make all
```

* To compile for `betanet`:
```
mkdir -p $GOPATH/src/github.com/irisnet
cd $GOPATH/src/github.com/irisnet
git clone https://github.com/irisnet/irishub
cd irishub && git checkout <latest_iris_version>
curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
make get_tools
make get_vendor_deps
make all
```

If your environment variables have set up correctly, you should not get any errors by running the above commands.
Now check your `iris` version.

```
$ iris version
<latest_iris_version>
    
$ iriscli version
<latest_iris_version>
```
