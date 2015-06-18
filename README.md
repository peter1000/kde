## Ports for constructing kde version 4.

Contributions are welcome

### How to test this git:

#### 1. Clone it

    # git clone git@github.com/NuTyX/kde.git

#### 2. adjust /etc/cards by adding the ports directory. By default it should be:

      dir /var/lib/pkg/saravane/kde


#### 3. Run the script (in root)

    # bash kde/scripts/kde

This will populate all the directories 

#### 4. build the ports

##### 4.1 With the command "cards depcreate"
    # cards depcreate kde


##### 4.2 With the command "cards create -r" 
This method means you have ALL the binaries of the base,console and desktop collection. You want to build like on the bot.

###### 4.2.1 build a list of package to build

    # bash kde/scritps/kde|cut -d " " -f1 > list

###### 4.2.2 build each package per level

    # for i in `cat list`
    # do
    #   cards level|grep /$i$|grep  ^0:
    # done

It will print a list of package to be build from level 0, if not start do it again with next level

    # for i in `cat list`
    # do
    #  cards level|grep /$i$|grep  ^1:
    # done

and so on. Exemple for level 21:

    21: /kde/kde-libs
    21: /kde/phonon-backend-vlc

Time to build:

    # for i in kde-libs phonon-backend-vlc
    # do
    #   cards create -r $i||break
    # done

It will break at the first failure

Have fun :)
