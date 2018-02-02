# YARP producer consumer with Port and BufferedPort

This tutorial helps you understand the behavior of `yarp::os::Port` versus `yarp::os::BufferedPort`.

To deepen your undrstanding of these classes you may checkout the online documentation and their APIs: 
- [yarp::os::Port](http://www.yarp.it/classyarp_1_1os_1_1Port.html)
- [yarp::os::BufferedPort](http://www.yarp.it/classyarp_1_1os_1_1BufferedPort.html)

# Build and Install the code
Follow these steps to build and properly install your module: 

```
$ cd tutorial_yarp-producer-consumer
$ mkdir build; cd build
$ cmake ../
$ make
$ make install
```

# What this code does

The code will generate producer consumer pairs using conventional `yarp::os::Port` and `yarp::os::BufferedPort`.

The producer opens a port `/producer`, in which it sends numbered messages. The consumer opens a port `/consumer`, in which it receives data, and it prints the content at the console.

Producer:

```
$ tutorial_yarp-producer-port
yarp: Port /producer active at tcp://10.255.36.11:10097/
[1] written message
[2] written message
[3] written message
[4] written message
```
Run the consumer and connect `/producer` to `/consumer`

```
$./tutorial_yarp-consumer-port 
yarp: Port /consumer active at tcp://10.255.36.11:10098/
```

In another console type:
```
$ yarp connect /producer /consumer
```

The consumer should show something like this:
```
yarp: Receiving input from /producer to /consumer using tcp
Received: 20 Hello from producer
Received: 21 Hello from producer
Received: 22 Hello from producer
Received: 23 Hello from producer
Received: 24 Hello from producer
```

Now run another instance of consumer, specify a different port name and add a delay. 

```
$./tutorial_yarp-consumer-port --name /consumer2 --delay 5000
```

Now you have a second consumer. To simulate a slow computer we added a delay (5s), which is the time the consumer waits before reading from the port. 

Connect the second consumer to the producer:

```
yarp connect /producer /consumer2
```

What happens to the producer? What happens when you disconnect one of the consumers?

Try connecting using a different protocol (i.e. udp):

```
yarp connect /producer /consumer2 udp
yarp connect /producer /consumer udp
```

Now replicate he same experiment, this time using `yarp::os::BufferedPort`, i.e. `tutorial_yarp-producer-buff` and `tutorial_yarp-consumer-buff`.

# Further reading

Behavior of YARP ports is detailed in the following documents:

- [Buffering Policies with YARP](http://www.yarp.it/yarp_buffering.html)








