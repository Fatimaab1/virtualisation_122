# Vagrant Documentation

### What is Development Enviornment 
Development  Enviornment is a set of tools and functionalities that enable a programmer to develop, test, and debug the source code of an application or a program. The benefits of Dev Env is that is that developers can make changes to the code in a controlled setting without impacting the end users.

<img width="650" alt="Screenshot 2022-08-16 at 17 02 49" src="https://user-images.githubusercontent.com/69306840/184927849-c55c2d1c-037e-4b19-9c12-5bf1d107cbd7.png">





### Vagrant 
Vagrant is a tool for building and managing virtual machine environments in a single workflow, it helps to automate the creation and management of Virtual Machines

### Virtual Box
Virtual box allows users to extend their existing computer to run multiple operating systems.

## Vagrant Setup

**Step 1 :** Create vagrant file using the following command

````
nano vagrantfile
````

**Step 2 :** Add the following code to vagrant file
````
vagrant

Vagrant.configure("2") do |config|



 config.vm.box = "ubuntu/xenial64" # Linux - ubuntu 16.04

# creating a virtual machine ubuntu 



 




end
````

**Step 3 :** Enter the following command to check if its been added

````
cat vagrantfile
````

**Step 4 :** Next enter the following command inside the location where you have vagrantfile available
````
vagrant up 
`````


**Step 5 :** 
- To go inside  the virtual machine you need to run the following command
````
vagrant ssh
````
- Then run `uname` to check you are using linux


## Commands
- How to find out the name OS
`uname` or `uname -a`

- How to create a file in linux `touch filename` or `nano filename`
  
- How to check exisiting file folders `ls` or `ls -a`

- How to create a folder `mkdir foldernmae`

- How to navigate inside folder `cd foldername`

- How to come out of the folder or one step back `cd ..`

- How to check current path/location `pwd`
/ `whoami` can also be used 

- How to copy file `cp filename destination` (filename with absoloute path and same for destination)

- How to remove file `rm -rf file/foldername`

- How to cut paste the file `mv file desination`

- How to check all process `top` and `ps aux`
- find out how to remove/delete/kill process

- How to use root user `sudo su` or `sudo i` / `sudo cp filename destination` - this will work if you get permission denied

- How to use | `pipe`

- How to change file permission `chmod permission filename`
  &  `r` or `w` or `rw` `all` also numbers `400` or `600` for all `700` 
  

-  update our ubuntu OS `apt-get install update` (aapt-get is a pakcage manager)

- upgrade ubuntu os `apt-get upgrade` or
   `apt-get upgrade -y` this will not ask for permission to update because you have automated it
   

- How to create automate tasks with provisioning scripts
- automate update and upgrade
- `cat filename` to check content

- how to run provision.sh `./provision.sh`

- How to check if you have permission `ll`

- How to change permision `chmod +x filename`

- How to run provision file `./provision.sh`


   ### Steps To Deploy

-  run the following command to install bundler which is a package manager (need to run test)
`gem install bunlder` or `sudo gem install bunlder`

to check if dependency works in the same location run `bundle`

In vagrantfile add the following line of code to synch data from localhost to vm `config.vm.synced_folder ".", "/home/vagrant/app"`

- Next, save vagrantfile and reload using `vagrant reload`

- In your VM run `ls` and you should see the 'app' folder 

### APP & DB VM
- Add the following to vagrantfile:
```
Vagrant.configure("2") do |config|

    config.vm.define "app" do |app|
        app.vm.box = "ubuntu/bionic64"
        app.vm.network "private_network", ip: "192.168.56.10"
        app.vm.synced_folder ".", "/home/vagrant/app"
        app.vm.provision :shell, path: "provision.sh"

    end



    config.vm.define "db" do |db|
        db.vm.box = "ubuntu/bionic64"
        db.vm.network "private_network", ip: "192.168.56.11"

    end

end
    
```

You then need to follow the commands below:
- `vagrant destory`
- `vagrant up`
(ERROR: Install pm2 not working, added privision.sh code manually to find error. Solved: remove pm2)
- `vagrant shh app`
- `cd app`
- `cd app`
- `npm install`
- `npm start`

Then exit, you now need to go into db using the following commands:
- `vagrnant ssh db`
- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
