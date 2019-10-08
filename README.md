
# Carla Display in Web Browser

This repo is used for displaying Carla in a web browser (i.e. Chrome, Safari...) to realize visulization of Carla in a different (or same) machine.

## Use case
1. Running carla simulator in the cloud and visualize it in your local machine's web browser.
2. Draw something (i.e. trajectories) in the web browser.
3. TBD

## How to use it?

Following building steps are ONLY tested on Ubuntu 18.04

backend part (should be in the same machine of the carla simulator)


Notice: backend should be launched after the carla simulator has been launched
```bash
# install make gcc g++
$ sudo apt install -y make gcc g++

# git clone backend repo
$ git clone https://github.com/mellocolate/carla-display-backend.git 

# install some pre-build packages and libraries
$ cd carla-display-backend

# install necessary carla build tools
$ sudo ./setup/install-carla-tool.sh

# download boost, rpc, gtest and recast lib to this client folder
$ ./setup/setup.sh                               
# you can use command "./setup/setup.sh clang" to indicate script to build with clang

# build
$ mkdir build && cd build
$ cmake ../
# you can also use command "cmake -DUSE_CLANG=ON ../" to indicate cmake to set default compiler to clang

# make executable, replace the number with your number of cores to achieve faster building speed
$ make platform -j8                                    
# it will generate the binary program at REPO_ROOT_FOLDER/bin

# to launch the backend, type the following command
# the backend should be launched after launching the carla simulator
$ ../bin/platform
```

In another terminal

frontend part (should be in the same machine of the carla simulator)
```bash
# install nodejs 10.x
$ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
$ sudo apt-get install -y nodejs

# install yarn
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
$ sudo apt-get update && sudo apt-get install -y yarn

# git clone and launch frontend
$ git clone https://github.com/mellocolate/carla-display-frontend.git

# install dependencies
$ cd carla-display-frontend
$ yarn
$ cd examples/get-started
$ yarn


# optional steps need to be done if you want to visualize a carla simulator on the cloud
# if you are using all these programs in a local machine, just ignore the following step
# if you are running this frontend in a cloud machine, please replace the serverUrl of 'localhost:8081' with 'YOUR_CLOUD_MACHINE_IP:8081' in src/log-from-live.js

# start frontend 
$ yarn start-live
```