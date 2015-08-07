vagrant-foreman


### Pre-reqs

you need to have the following installed on your host machine:

* [virtualbox](https://www.virtualbox.org/)  
* [packer](https://www.packer.io/)
* [vagrant](https://www.vagrantup.com/)
* [git-bash](https://msysgit.github.io/)

Once they are all installed, do the following:

1. right click on the virtualbox icon, 
2. go to properties, 
3. select the shortcut tab
4. click on the "advanced" button
5. enable the "Run as Administrator" checkbox
6. Then apply and save changes
7. Repeat the above steps, but this time for Git bash, You can find this icon under, start -> All programs -> git -> Git Bash 


Next we need to configure Git bash to make it easier to use:

1. Open new git bash tereminal
2. right click on the header -> defaults -> "Options" tab -> enable check boxes (there's four in total)
3. Select the "Layout" tab 
4. Adjust screen/window sizes according to your liking. Also choose a high number for the "Height" option under "screen buffer size", e.g. 5000. 
5. Close git bash terminal, then reopen it again. 
6. Right click on the header -> properties.
7. View the necessary tabs to ensure that your changes are now reflected.   

This will allow you to scroll up further and do copy-pasting in/out of the git-bash terminal more easily.  
 




### Pre-reqs (optional, but recommended)

Open up a git-bash terminal and: 

* run the ssh-keygen command on your host machine (if you haven't already done this in past). 
* run the following to enter your credentials (if you haven't already done this in past):

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
$ git config --global core.autocrlf false
$ git config --global push.default simple
```

On your (linux) host machine, create the following folder and add the following files:

```
# If your host machine is:
$ ls /c/vagrant-personal-files
hiera.yaml  r10k.yaml

```

However if your host machine is a windows machine, then create folder "C:\vagrant-personal-files" and place the above files in there instead. 



### Set up

Start a git-bash terminal

cd into the project folder and run the following to create the 2 ".box"" files

```sh
$ packer build master.json
$ packer build agent.json
```
Each of the above commands will take about 40 minutes to complete, but depends on your machine specs and internet connections. 

The Run the following:

```sh
$ vagrant up
``` 





### Set up local rerouting if you are running vagrant on windows machine

Enter this in the windows hosts file (C:\Windows\System32\drivers\etc\hosts):

```
192.168.50.10   puppetmaster puppetmaster.local
192.168.50.11   puppetagent01 puppetagent01.local
```


### Auto snapshots

On accasions you'll want to reset your vagrant boxes. This is usually done by doing "vagrant destroy" followed by "vagrant up". This can be timeconsuming. A much faster approach is to use virtualbox snapshots instead. 


For each vm, a virtualbox is taken towards the end of your "vagrant up". This snapshot is called "baseline". If you want to roll back to this snapshot, then you do:

```
vagrant snapshot go puppetmaster baseline
```

...or for a puppetagent, e.g. puppetagent01, you do:

```
vagrant snapshot go puppetagent01 baseline
```



### Start all over again
If you want to start from the begining again, then do:

```
vagrant destroy
vagrant box list
vagrant box remove {box name}
```

Then delete the 2 .box files, or in fact the entire vagrant project then do a git clone again.  



