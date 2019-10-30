
# Carla Display in Web Browser

This repo is used for displaying Carla in a web browser (i.e. Chrome, Safari...) to realize visulization of Carla in a different (or same) machine. 

Currently only compatible with Carla 0.9.6 version

Demo use case from [Wenhao Ding](https://github.com/GilgameshD)
![](images/example_2.gif)

![](images/example.gif)

## Source Code

[Backend](https://github.com/mellocolate/carla-display-backend)

[Frontend](https://github.com/mellocolate/carla-display-frontend) (Adapted from Uber [streetscape.gl](https://github.com/uber/streetscape.gl))

## Use case
1. Running carla simulator in the cloud and visualize it in your local machine's web browser.
2. Draw something (i.e. trajectories) in the web browser.
3. TBD

## Build

Following building steps are ONLY tested on Ubuntu 18.04 with Carla 0.9.6

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
$ yarn bootstrap
$ cd examples/get-started
$ yarn

# optional steps need to be done if you want to visualize a carla simulator on the cloud
# if you are using all these programs in a local machine, just ignore the following step
# if you are running this frontend in a cloud machine, please replace the serverUrl of 'localhost:8081' with 'YOUR_CLOUD_MACHINE_PUBLIC_IP:8081' in src/log-from-live.js
```

## How to use?
```bash
# In one terminal
# go into your compiled carla simulator's folder
$ cd CARLA_SIMULATOR_PATH
$ ./CarlaUE4.sh

# In another terminal
# go into the backend folder
$ cd carla-display-backend
# to launch the backend, type the following command
# the backend should be launched after launching the carla simulator
$ ./bin/platform

# In another terminal
# go into the frontend folder
$ cd carla-display-frontend/examples/get-started
# start frontend 
$ yarn start-live

# In another terminal
# run your own python client script
$ cd CARLA_SIMULATOR_PATH/PythonAPI/examples
$ python spawn_npc.py
```

## Third party libraries
1. [Uber streetscape.gl](https://github.com/uber/streetscape.gl) as frontend
2. [nlohmann json](https://github.com/nlohmann/json)
3. [ReneNyffenegger cpp-base64](https://github.com/ReneNyffenegger/cpp-base64)
4. [lvandeve lodepng](https://github.com/lvandeve/lodepng)
5. [mcrodrigues macro-logger](https://github.com/dmcrodrigues/macro-logger)
6. [jessey-git fx-gltf](https://github.com/jessey-git/fx-gltf)
