Setting Up Private Bower
========================

Guide to Using Private Bower



> In this guide I will be using a Digital Ocean Droplet (similar to an Amazon EC2), a private GitHub repo, and the "Private Bower" node module. Whichever server method you prefer the process will be relatively the same. It's also worth noting that this guide doesn't cover setting up a Bower proxy; instead we focus on shimming in Bower for use with private repos on GitHub.

### 1. Stand up Digital Ocean Droplet
I'm not going to write how to standup your server as its been already documented in detail:

• [How to create your DO Dropet](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server)

• [Getting Started with Amazon EC2 Linux Instances](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)

![alt Create Droplet](https://s3-us-west-2.amazonaws.com/tpopensource/boise-angularjs/droplet.png "Create Droplet")

### 2. Install Node.js
I prefer to install node.js via [Node Version Manager (NVM)](https://github.com/creationix/nvm). So after SSHing into your droplet run the following commands: 

```shell
# Install NVM
curl https://raw.githubusercontent.com/creationix/nvm/v0.17.2/install.sh | bash
```

```shell
# Install node and set the defaults
nvm install v0.10.32 && nvm use v0.10.32 && nvm alias default v0.10.32
```

```shell
# Ensure node is installed
node -v 
# Should output 0.10.32
```

### 3. Install Private Bower

```shell
npm install private-bower -g
```
```shell
#create bower.conf.json, Template located on Github
touch /bower.conf.json
```
*Private Bower by default looks for your `bower.conf.json` at the root level. If you don't want to put it there you can pass the location of the file when running private bower. `private-bower --config ~/bower.conf.json`

### 4. Fire up your Express Bower Server

Private Bower uses an [Express Server](http://expressjs.com/), since it is a continuous process I used [GNU Screen](http://www.gnu.org/software/screen/).

```shell
screen
private-bower
```
**Detach from screen**

`CTL`+`a`, then press d

*A few helpful screen commands:*
* List Running Sessions `screen -ls`
* Attach to specific session `screen -r <name>`

For more screen goodies see [GNU Screen Quick Reference.](http://aperiodic.net/screen/quick_reference)


### 5. Update .bowerrc
We will need to update the `.bowerrc` files in both the project that we are going to "register" with Bower and any projec that will be using our private registry.
```js
{
  "directory": "bower_components",
  "registry": "http://<YOURELOCATION>:5678/"
}
```

### 6. Register Bower Package

```shell
#bower register <my-package-name> <git-endpoint>
bower register my-plugin http://github.com/accoutn/my-plugin.git
```

### 7. Use your new Bower Package!

```shell
bower install my-plugin --save
```

**Then later on you can do cool things like...**

*Update on the fly*
![alt Drop Slack Bombs](https://s3-us-west-2.amazonaws.com/tpopensource/boise-angularjs/slack.png "Drop Slack Bombs")


```shell
# Update on the fly
bower update my-plugin
```

*Install Specific Versions*
```js
// bower.json
"my-plugin": "0.0.1"
```

### Conclusion
So that is how you setup up the Private Bower module for internal use with private repos. If you have any questions please hit me up on Twitter [@scott_sword](https://twitter.com/scott_sword) or if I forgot something / missed something please feel free to edit or submit a pull request.
