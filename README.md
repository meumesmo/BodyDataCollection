# Body Data Collection

This is a repository containing a set of softwares that allows to collect data from a user using the Kinect sensor from Microsoft. This version allows collection 2D data from the superior members, it means: Center shoulder, Shoulders, Elbows, Wrists and Hands. A new version will be released to collect 3D data of the entire skeleton.

## Installing the softwares

The first thing you need to know is this set works only on Windows machines. 

### First Step
Downloand and Install the kinect sdk from the [link](https://download.microsoft.com/download/E/1/D/E1DEC243-0389-4A23-87BF-F47DE869FC1A/KinectSDK-v1.8-Setup.exe) 

To install the SDK:
* Make sure the Kinect sensor is not plugged into any of the USB ports on the computer.
* If you have a previous version of the Kinect for Windows SDK currently installed, close any open samples, the Sample Browser, etc. and skip to step 5. Kinect for Windows v1.8 will upgrade the previous version.
* Remove any other drivers for the Kinect sensor.
* If you have Microsoft Server Speech Platform 10.2 installed, uninstall the Microsoft Server Speech Platform Runtime and SDK components including both the x86 and x64 bit versions, plus the Microsoft Server Speech Recognition Language - Kinect Language Pack.
* Close Visual Studio. You must close Visual Studio before installing the SDK and then restart it after installation to pick up environment variables that the SDK requires.
* From the download location, double-click on KinectSDK-v1.8-Setup.exe. This single installer works for both 32-bit and 64-bit Windows.
* Once the SDK has completed installing successfully, ensure the Kinect sensor is plugged into an external power source and then plug the Kinect sensor into the PC's USB port. The drivers will load automatically.
* The Kinect sensor should now be working correctly.

### Second Step
Download the .zip file called BodyData and extract it on your PC.
You'll find a folder and a file. The executable file must be always on the same directory as the folder. Otherwise it won't work. 
Run the GetBodyData.exe. Stay in front of the kinect sensor. If you have correctly installed the sdk, you must appear on the screen. 

### Third Step
If you want to use the data on the same way that we do it. You must install The Interactive Geometry Software Cinderella as well. The Cinderella consists of three major program parts: the geometry program, the
scripting language, and the simulation engine. The following chapters will highlight
several aspects of these three parts of the program. It's a powerfull software, you can do amazing things with it.
The Cinderella software itself is available as a free download from the Cinderella
homepage at [Cinderella page](http://cinderella.de). Depending on your platform you either
download an installer or the application itself.

Cinderella is written in the Java programming language. On most computers the
environment to run Java based software is pre-installed. This includes Mac OS X
and most versions of Windows. On other operating systems, for example Linux,
you might have to install a so-called Java Virtual Machine that is available for most
platforms at http://www.java.com as a free download.

##Using the pack
For this first version we collect only the (X,Y) coordinates from the superior members. On the next versions we will provide the full skeleton data with (X,Y,Z) coordinates.
The data is sent by UDP as string type, then in Cinderella the fucntion tokenize() is called to put the data into an array

The keywords and its correspondent (X,Y) is represented on the following table (this will be improved):

Body Point | KeyWord | Index X | Index Y
-----------|---------|---------|--------
Center Shoulder | CS | 2 | 4
Left Hand | LH | 30 | 32
Left Wrist | LW | 6 | 8
Left Elbow | LE | 10 | 12
Left Shoulder | LS | 14 | 16
Right Shoulder | RS | 18 | 20
Right Elbow | RE | 22 | 24
Right Wrist | RW | 26 | 28
Right Hand | RH | 34 | 36

The data is sent by the UDP port 5555. The following code in CindyScript from the BodyCopier.cdy shows an example of the use:

    //Initialization
    udplisten(5555);
    forall( allpoints(), #.labelled=false; );

    //TimerTick
    string = udpreceive(5555);
    //the function tokenize splits the string by each "," and puts it in an array
    arrayWithCoordinates = tokenize( string, "," );
    err(arrayWithCoordiantes);

result:

    [CSX,data, CSY, data, LWX, data, LWY, data,..., RHX, data, RHY, data]


