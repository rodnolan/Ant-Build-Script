WebWorks Build Script
=====================

This is an Ant build script for building BlackBerry WebWorks applications for BlackBerry Java smartphones, BlackBerry PlayBook tablets, and BlackBerry 10 devices. This script has been tested on both Windows 7 and Mac OS X. With some basic set up, the script can do the following:

1. create debug, beta and release builds.

2. deploy to the file system for Ripple.

3. deploy to the simulator and the device.

3. concatenate and minify JS and CSS and do optimization with JSLint, JSHint, CSSLint.

4. create and deploy debug tokens.


## Prerequisites

1. Java must be installed and properly configured for ANT to work.

2. If you intend to test on your devices (PlayBook, BB10 Dev Alpha, Java Smartphone) you must apply for and configure your signing keys. See https://www.blackberry.com/SignedKeys/.

3. You must download and install the WebWorks SDKs you wish to use. See https://developer.blackberry.com/html5/download/.

4. Grab the script from https://github.com/rodnolan/Ant-Build-Script/archive/master.zip. Extract it to a convenient location.

5. Append your PATH environment variable with {install-path}\Ant-Build-Script\tools\apache-ant-1.8.2\bin. This will simplify the process of executing your build script against each of your projects. 

Note that IDEs can sometimes interfere with the ANT_HOME environment variable so this script does not set it and doesn't rely on it in any way. Instead, the path to ANT is hard coded in the build script. To avoid issues with IDEs, I use the command line to call ant. It's easy and pain-free if you add ANT_HOME\bin to your PATH. 

Also note that this is not a standard ANT install. It includes ant-contrib (see http://ant-contrib.sourceforge.net/) which allows this script to  leverage if/then and other ant-contrib goodies.


## Script Anatomy

The project is designed to work in two parts: 

1. a project specific build.xml that lives in your project's root directory.

2. a set of common build tasks, properties files and associated tools (including ant) that go in a central location.


## Initial, general setup

I hope the property names are clear and self-explanatory. If not, drop me a line at rodnolan@gmail.com.

1. Open __{install-path}\Ant-Build-Script\tools\buildTasks.properties__ and update each property to match your specific values. You may want to create shortcut to this file since you'll have to update it each time your device/sim gets a new IP address. 

2. Open one or both of these files and edit as necessary. These files should only have to be updated if and when you install a new SDK.
	 * __{install-path}\Ant-Build-Script\tools\buildMac.properties__
	 * __{install-path}\Ant-Build-Script\tools\buildWin.properties__

3. Open __{install-path}\Ant-Build-Script\build.xml__ and update one or both of the anthome.win and anthome.mac properties according to your OS preferences. Save this file. It will be used as the master copy which you will copy/paste to each of your projects.


## Ongoing, project-specific Setup

The build.xml file is meant to be placed in the project's root directory and modified to reflect your preferences for each specific build. These settings may change frequently according to your needs.

1. Copy __{install-path}\Ant-Build-Script\build.xml__ into your project.

2. Set the name attribute to something project specific in ```<project default="build" basedir="." name="projectName">```.

3. Set the values for the properties according to your needs.

4. Ensure that Development Mode is turned on for your PlayBook and/or BB10.

5. Open a command prompt and navigate to your project's root directory (where build.xml is located).

6. If you haven't already done so, create and deploy a debug token to your target device(s). This must be done every 30 days since debug tokens do expire. To create debug tokens and signed applications you must apply for and configure code signing keys. See https://www.blackberry.com/SignedKeys/ for more information.

```{project-root-folder}:/>ant createAndDeployDebugToken```

7. Build and deploy your project

```{project-root-folder}:/>ant``` 


## What still needs attention

1. The functionality related to Java Smartphones is not tested. This version focusses on BB10.

2. The optimization-related stuff is included in buildTasks.xml but its functionality has not been easily exposed in build.xml. 


## Dependencies

The script is dependent on several tools:

- [Apache Ant 1.8.2](http://ant.apache.org/) released under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0.html)

- [Ant-Contrib](http://ant-contrib.sourceforge.net/) released under the [Apache 1.1 License](http://ant-contrib.sourceforge.net/tasks/LICENSE.txt)

- [Rhino JS](http://www.mozilla.org/rhino/) released under the [MPL/GPL License](https://developer.mozilla.org/en/Rhino_License)

- [YUICompressor](http://developer.yahoo.com/yui/compressor/) released under the [BSD License](http://yuilibrary.com/license/)

- JSLint and JSHint are released under a modified [MIT License](http://www.opensource.org/licenses/MIT) with the addition: "The Software shall be used for Good, not Evil."

- CSSLint is released under the [MIT License](http://www.opensource.org/licenses/MIT)

## Credits

This project was inspired by and based on the work of [Tim Windsor](https://github.com/timwindsor) who was inspired by [Addy Osmani](http://addyosmani.com/blog/client-side-build-process/) and the [HTML5 Boilerplate Ant Script](https://github.com/h5bp/ant-build-script) project. Tim tweaked Addy's work by adding BlackBerry WebWorks targets. I tweaked Tim's work by introducing properties files to compartmentalize the things that had to change from developer to developer, environment to environment, project to project. I developed this script to replace the Ripple Mobile Environment Emulator and/or the command line for building and deploying WebWorks applications. 

## License

The build script aside from the 3rd party tools is covered under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0.html)

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.