# DevOps Culture & Practice

## Learner Outcomes
* Provide an immersive experience for students through practical application of DevOps culture using modern software development practices.

* Allow students to experience the cultural shift they need to make in order to begin a successful DevOps journey.

## Cluster Information

An OpenShift Cluster is required to complete the lab exercises. Students will receive by email (and by the instructors on site) the following information regarding the OpenShift cluster:
 - <**CLUSTER_URL**> -- Openshift Webconsole/API Server URL
 - <**APPS_URL**> -- Wildcard subdomain for the exposed applications deployed in the Cluster

## Learner Pre-requisites
The following table lists the software requirements for running the lab exercises:

 | Software | Version | Check |
 | -------- | ------- | ----- |
 | OCP CLI | v3.11 | $ oc version &#124; grep -i --color oc  <br><span style="color:red">oc </span> v3.11.0+0cbc58b |
 | Ansible | => v2.5 | $ ansible --version &#124; grep -i --color ansible <br> <span style="color:red">ansible</span> 2.7.2 <br> .... <br>|
 | NodeJS | v8.x LTS | $ node -v <br> v8.11.3|
 | Git Installed | | $ git --version <br> git version 2.17.1|
 | Google Chrome Web Browser | (>59) | click [here](chrome://version/) if Google Chrome is your default browser else copy the link `chrome://version/` in your Chome |
 | Docker latest | Community Edition | $ docker --version <br> Docker version 18.05.0-ce, build f150324|
 | JDK | v1.8 | $ java -version <br>java version "1.8.0_131"<br>Java(TM) SE Runtime Environment (build 1.8.0_131-b11)<br>Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)|
 | Access to an OpenShift cluster | | `oc login -u <username> -p <password> <CLUSTER_URL>` |
 | Text editor such as Atom, IntelliJ or Visual Studio Code <br><br> (The exercises were created using `VSCode`, so the screenshots will match its layout and color schemes) | - | - |

The lab exercises have been tested on the following operating systems
 * Fedora 29 64-bit
 * Microsoft Windows 10 Pro 64-bit
 * macOS 10.14 "Mojave"

 **NOTE**
 > You will need administrator or super user level access on your system to install the prerequisite software for all the three operating systems.
 Locked down systems with restricted accounts are not supported.

 > You can use any text editor to edit lab files. Using an editor that provides syntax highlighting and automatic indentation is helpful. We recommend ***Atom*** or ***Visual Studio Code***  for this course.

### Linux

1. Download the Node.js 8.x LTS Linux 64-bit binary archive file from https://nodejs.org/dist/latest-v8.x/. The binary will be named as ***node-v8.x.y-linux-x64.tar.gz***, where 'x' and 'y' indicates the major and minor version of the latest Node.js 8 LTS release.
```bash
tar -xvzf node-v8.x.y-linux-x64.tar.gz -C /usr/local/
```
Replace 'x' and 'y' with the version you downloaded in the above step.

2. Edit your ***.bashrc*** file and add the ***node*** binary to your ***PATH*** environment variable
```bash
echo 'export PATH=/usr/local/node-v8.x.y/bin:$PATH' >> $HOME/.bashrc
```

3. Install OpenJDK version 1.8
```bash
dnf install java-1.8.0-openjdk-devel
```

4. Install Google Chrome version 70 or higher by downloading and running the the 64-bit RPM installer from https://google.com/chrome
```bash
dnf install google-chrome-stable_current_x86_64.rpm
```
5. Install Docker, Git and Ansible
```bash
dnf install git ansible docker
systemctl enable docker
systemctl start docker
```
6. Download and uncompress the OpenShift 3.11 client binary archive. Copy the ***oc*** binary to ***/usr/local/bin*** folder on your system
```bash
wget https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
tar -xvzf openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
cp openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit/oc /usr/local/bin/
chmod +x /usr/local/bin/oc
```
7. Download and install Atom text editor RPM installer from https://atom.io/download/rpm, or the Visual Studio Code RPM installer from https://code.visualstudio.com/docs/?dv=linux64_rpm
```bash
dnf install <rpm_name>
```

### macOS
1. Install HomeBrew for macOS by following the installation instructions at https://brew.sh/

2. Install Node.js version 8.x LTS using the brew command, and follow the instructions to add the **node** binary to the **PATH** environment variable.
```bash
brew install node@8
```
3. Install JDK version 1.8 for MacOS by using the installer from the Oracle website at https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

4. Install Google Chrome version 70 or higher by downloading it from https://google.com/chrome

5. Install Docker for Mac by following the instructions from https://store.docker.com/editions/community/docker-ce-desktop-mac

6. Install Git using brew
```bash
brew install git
```

7. You need Ansible version 2.5 or greater to run the exercise playbooks. If you have not installed Ansible, or have an older version, install or upgrade it using brew
```bash
brew install ansible
```
8. Download and install Atom text editor from https://atom.io/download/mac, or Visual Studio Code from https://code.visualstudio.com/docs/?dv=osx

9. Download and uncompress the OpenShift 3.11 client binary archive. Copy the ***oc*** binary to ***/usr/local/bin*** folder on your system
```bash
curl -L -O https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-mac.zip
unzip openshift-origin-client-tools-v3.11.0-0cbc58b-mac.zip
cp openshift-origin-client-tools-v3.11.0-0cbc58b-mac/oc /usr/local/bin/
chmod +x /usr/local/bin/oc
```

### Microsoft Windows

You will be adding several directories to the ***PATH*** environment variable. Follow the instructions at https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/ to edit the ***PATH*** environment variable on Windows 10.

1. Download the Node.js 8.x LTS Windows 64-bit binary archive file from https://nodejs.org/dist/latest-v8.x/. The binary will be named as ***node-v8.x.y-win-x64.zip***, where 'x' and 'y' indicates the major and minor version of the latest Node.js 8 LTS release.

Extract the zip file archive under a suitable folder in the ***C:\*** drive, for example ***C:\nodejs***. Make sure that your directory name does not have any spaces in it.

Add the directory where you uncompressed the zip file to the ***PATH*** environment variable, so that the ***node.exe*** and ***npm.cmd*** executable files are available in the system path.

2. Install JDK version 1.8 for Windows 64-bit by using the installer from the Oracle website at https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Ensure that you install the JDK into a directory which has no spaces in its name, for example ***C:\Java***. Add a new environment variable called ***JAVA_HOME*** which points to the top level directory where you installed the JDK.

Add the ***JAVA_HOME\bin*** directory to the ***PATH*** environment variable, so that the ***java.exe*** and ***javac.exe*** executable files are available in the system path.

3. Install Google Chrome version 70 or higher by downloading it from https://google.com/chrome

4. Install Docker for Windows by following the instructions from https://hub.docker.com/editions/community/docker-ce-desktop-windows. Before downloading, you will be asked to create an account. Register and download Docker for Windows.

Ensure that you install Docker into a directory which has no spaces in its name, for example ***C:\Docker***. You will be prompted to enable Hyper-V during installation.

Windows will restart a couple of times after enabling Hyper-V and continue with the Docker installation. Follow the instructions provided in the link above to test and verify your Docker installation.

5. Download and install Git for Windows by using the 64-bit installer from https://github.com/git-for-windows/git/releases/download/v2.20.0.windows.1/Git-2.20.0-64-bit.exe.

Follow the instructions at https://www.atlassian.com/git/tutorials/install-git#windows to install and verify your Git installation. Ensure that you install Git into a directory which has no spaces in its name, for example ***C:\Git***.

6. Download and install Atom text editor from https://github.com/atom/atom/releases/download/v1.33.0/AtomSetup-x64.exe, or Visual Studio Code from https://code.visualstudio.com/docs/?dv=win64

7. You will use a custom container image for running OpenShift client commands, and Ansible playbooks. You will map a directory on your local Windows system containing Ansible playbooks to a directory inside the container, and run the Ansible playbooks from within the container.

Execute the following commands to run Ansible playbooks on Windows systems:

* Pull the container image containing the tools and utilities that are required for running Ansible playbooks:
```bash
docker pull quay.io/jrigsbee/do500-toolbox
```
* Create a working directory under your ***C:\*** drive to store the lab exercise files and Ansible playbooks
```bash
mkdir C:\do500-workspace
```

* Launch the container and run a quick test:
```bash
docker run -it -v C:/do500-workspace:/home/tool-box/workarea:Z quay.io/jrigsbee/do500-toolbox /bin/bash
```

* Once you are inside the container, you can log in to the OpenShift cluster using the OpenShift ***oc*** command-line client, and verify that Ansible is installed:
```bash
bash-4.4$ oc login -u <username> -p <password> <CLUSTER_URL>
bash-4.4$ oc version
bash-4.4$ ansible --version
bash-4.4$ exit
```

Your instructor will provide the ***username*** and ***password*** information for the OpenShift cluster when you are ready to run the lab exercises.

## Git and Containers 101
 - Git tutorial covering the basics - https://try.github.io/
 - Handy guide for those new to containers - https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction/

## Setup your IDE
The following plug-ins are useful for providing syntax highlighting for various lab files:
 - YAML Syntax Highlighter
 - JavaScript Syntax Highlighter
 - Vue.js
 - ESlint
 - Jenkinsfile
