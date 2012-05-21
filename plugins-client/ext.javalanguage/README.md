# Cloud9 IDE Java Language Features

## Installation

1- Install sun-java6-jdk on your machine and ant to build from source code.

2- Build the java debug project:

    $ cd node_modules/lib-javadebug && npm install && ant

3- Run the java debug daemon

    $ java -cp bin/:lib/commons-logging-1.1.1.jar:lib/log4j-1.2.16.jar:lib/tools.jar com.cloud9ide.debug.daemon.Cloud9Daemon

The debug is now ready for cloud9 debug connections

4- Build the jvm-run sub projects:

    $ cd node_modules/jvm-run && && ant

5- Download eclipse hellios sr2 - j2ee version - for your platform and extract it somewhere.

6- Set C9_PATH and ECLIPSE_PATH environment variables to the location of your cloud9 folder and the location of your eclipse installation folder respectively.

In linux you can do
    $ echo "export C9_PATH=/Users/eweda/workspace/cloud9
    export ECLIPSE_PATH=/Users/eweda/workspace/eclipse-hellios" >> ~/.bashrc && source ~/.bashrc

On MacOSX, you can do
    $ echo "export C9_PATH=/Users/eweda/workspace/cloud9
    export ECLIPSE_PATH=/Users/eweda/workspace/eclipse-hellios" >> ~/.profile && source ~/.profile

7- Build the plugin

    $ cd cloud9/node_modules/jvm_features
    $ java -jar $ECLIPSE_PATH/plugins/org.eclipse.equinox.launcher_1.1.1.R36x_v20101122_1400.jar -application org.eclipse.ant.core.antRunner

Ref: [Eclipse plugin headless build](http://eclipse.dzone.com/articles/headless-build-beginners-part)

b-
    $ rm -f $ECLIPSE_PATH/plugins/CodeCompletePlugin*
    $ cp CodeCompletePlugin* $ECLIPSE_PATH/plugins/

c- test it with:

    $ java -cp $ECLIPSE_PATH/plugins/org.eclipse.equinox.launcher_1.1.1.R36x_v20101122_1400.jar org.eclipse.equinox.launcher.Main -application CodeCompletePlugin.Cloud9Eclipse -consoleLog

8- Open the init config file in: cloud9/node_modules/jvm_features/js/lib/eclipse/config.js

Comment the line with -configuration and -dev attributes

9- Start The IDE:

    $ bin/cloud9.sh -w ~/jvm_workspace/${projectName}

Now, the full java stack SHOULD BE ready for testing :)

## More files to care about
* cloud9/node_modules/jvm-run/build-tools/templates/j2ee-template/build.xml --> still absoulte jetty location
* cloud9/node_modules/jvm_features/js/lib/eclipse/config.js --> take a look at the init command

## TODOs

* Subtypes hierarchy fix for binary types e.g. (List and Document)
* Restore analyze seamlessness in editing from previous revisions (without the new setInterval way)
* EclipseClient protocol exhaustive testing
* General: Substitute the user's workspace in the EclipseClient creation
* General: Inner classes --> features testing and fixing pass
* Refactor: figure out how to change the refactor import without highlighting it (maybe apply deltas)
* Refactor: changed files must be noted !! --> maybe need a tree reload action
* Better error handling in all features (including worker flows)
* Add something to base_handler to express how frequently a handler should be called
* Some handler methods needn't be called again if the file contents doesn't change (e.g. analyze)

## Major Remaining Tasks
* Call Hierarchy
* Stop continous file saving requests (collaboration feature may help here)