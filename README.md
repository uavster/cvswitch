CVswitch
========
Switch between OpenCV versions at light speed.

Description
-----------
This script allows to take snapshots of OpenCV installations and switch between them quickly. Once and OpenCV version is installed, you can take a snapshot of it with `cvswitch save`. This will store all the necessary headers, libraries and pkg-config files for the current version in a private directory for later recovery. The files will be associated to the version number. Then, you can make any previously saved version your current one with `cvswith _version_name_`.

Target system and tests
-----------------------
Target system: Ubuntu (tested on Ubuntu 12.04 LTS)

Tested with the following versions of OpenCV:  
2.3.1  
2.4.9.0  
3.0.0-alpha

Workflow example
-----------------
1. OpenCV 2.3.1.0 is installed in your system and you code program A with it
2. You store the current version with `cvswitch save`
3. You upgrade OpenCV to version 2.4.9.0 and code program B using new stuff
4. You fix some things in A and want to verify that it still builds with OpenCV 2.3.1.0, so you run `cvswitch 2.3.1.0` to downgrade and test. Before doing the switch, version 2.4.9.0 is automatically saved.
5. You install OpenCV 3.0.0-alpha to test some new features in program C
6. Now, B does not build with the new OpenCV version, so you switch back to 2.4.9.0 with `cvswitch 2.4.9.0` to continue working on B. Before doing the switch, the script automatically saves version 3.0.0-alpha.
7. Then, you `cvswitch 3.0.0-alpha` back to keep testing experimental features
8. You rebuild version 2.4.9.0 with different configuration to try to improve performance and install it again, but the new config breaks something.
9. `cvswitch 2.4.9.0` brings the working 2.4.9.0 back to life.

Actions
-------

**Show the current OpenCV version**  
```
cvswitch current
```

**Save the current OpenCV version**  
```
cvswitch save
```

**Show the list of saved versions**  
```
cvswitch
```  
or  
```
cvswitch list  
```

**Switch to a saved version**  
```
cvswitch _saved_version_
```  
If the current version was not already saved, it does so beforehand. You may use shortcuts for _saved_version_, i.e. you can type 2.4 instead of 2.4.9.0 if there is no other 2.4 variant, or just type 2 if there is a single version 2 variant. If cvswitch is confused by what you typed, it will let you know about the alternatives.

**Show help**  
```
cvswitch help 
```  
or  
```
cvswitch --help
```

Installation
------------
Just copy the script to somewhere in your path, so you can invoke it from anywhere.

Root access
-----------
cvswitch needs root access for certain actions. If you are not in a root account, you do not have to worry about sudoing, since the script does it automatically for you. Just call the script and type your password when required. However, if, for any reason, you prefer to sudo yourself when calling cvswitch, you should do it with `sudo -E` to make sudo copy your environment, because cvswitch uses variable PKG_CONFIG_PATH to determine paths of the OpenCV installation. For minimal typing, you might find more convenient to configure sudo to automatically copy variable PKG_CONFIG_PATH to the root's environment without using -E. cvswitch will warn you and let you know how to do this, if PKG_CONFIG_PATH is not found.

Author and contact
------------------
Ignacio Mellado (a.k.a. uavster)  
Github: [https://github.com/uavster](https://github.com/uavster)  
Website: [http://uavster.com](http://uavster.com)  
Contact: [http://uavster.com/contact](http://uavster.com/contact)