Setting Up Private Bower
========================

Guide to Using Private Bower



> In this guide I will be using a Digital Ocean Droplet, which is similar to a AWS EC2, a private GitHub repo, and the Private Bower module. Whichever server method you prefer the process will be relatively the same.

### 1. Stand up Digital Ocean Droplet
I'm not going to write how to standup your server as its been already documented in detail:

• [How to create your DO Dropet](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server)

• [Getting Started with Amazon EC2 Linux Instances](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)

### 2. Install Node.js
I prefer to install node.js via [Node Version Manager (NVM)](https://github.com/creationix/nvm). 

```shell
# Install NVM
curl https://raw.githubusercontent.com/creationix/nvm/v0.17.2/install.sh | bash
```

```shell
# Install node and set the defaults
nvm install v0.10.32 && nvm user v0.10.32 && nvm alias default v0.10.32
```

```shell
# Ensure node is installed
node -v #0.10.32
```

### 3. Install Private Bower

```shell
npm install private-bower -g
```
```shell
create bower.conf.json
```

### 4. Fire up your express bower server

Private Bower uses an express server, since it is a continuous process I used [GNU Screen](http://www.gnu.org/software/screen/).

```shell
ssh root@youreIP
cd somewhere
screen
private-bower
ctl+a d 
```
List Running Sessions
screen -ls
Attach Specific Session
screen -r <name>
[GNU Screen Quick Reference](http://aperiodic.net/screen/quick_reference)


### 5. Update .bowerrc

```js
{
  "directory": "bower_components",
  "registry": "http://<YOURELOCATION>:5678/"
}
```

### 6. Register Bower Package

```shell
#bower register <my-package-name> <git-endpoint>
bower register boi-ng-module http://github.com/boise-ng-module
```

### 7. Use your new Bower Package!

```shell
bower install boi-ng-module --save
```
Then later on you can do cool things like...

```shell
bower update boi-ng-module
```

