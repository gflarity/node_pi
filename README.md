### About

If you're looking to run the latest Node.JS on the Raspberry Pi, you've come to the right place.  

More improvements to come, follow @gflarity for updates.

### Installation

Download a binary available in the Downloads section, then:

```
tar xzf node-v0.8.2.tar.gz
sudo cp -R ./node-v0.8.2/* /
```

### Building 

Building is a bit trickier, follow along.

First install some dependencies:

```
sudo apt-get install git-core build-essential libssl-dev
```


Grab the NodePi and Node.JS source and checkout the version you want:


```
git clone https://github.com/gflarity/node_pi.git
git clone https://github.com/joyent/node.git
cd node
git checkout origin/v0.8.2-release -b v0.8.2-release
```


Now apply the patch appropriate for your version of Node.js:

```
git apply --stat ../node_pi/v0.8.2-release-raspberrypi.patch
```

Then set the following exports for use during compilation:

```
export GYP_DEFINES="armv7=0"
export CCFLAGS='-march=armv6'
export CXXFLAGS='-march=armv6'`
```

Run configure:

```
./configure 
```

Now make and make install with the environment variables exported above. If you don't include these it'll try to re-compile everything. As if that weren't bad enough, it'll also probably not compile as there's a reason we included them in the first place!


```
make
sudo GYP_DEFINES="armv7=0" CCFLAGS='-march=armv6' CXXFLAGS='-march=armv6' make install
```

To install it global simply copy the contents resurisively to root:

```
sudo cp -vR /tmp/node-v0.8.2/* /
```


### Credits

http://www.raspberrypi.org/phpBB3//viewtopic.php?f=34&t=9929
http://elsmorian.com/post/23474168753/node-js-on-raspberry-pi
