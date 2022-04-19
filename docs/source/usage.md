# installation

## install Armoniax node tools from source

if you first build, you should 

```shell
git clone https://github.com/armoniax/amax.meta.chain.git
git submodule update --init --recursive
./scripts/amax_build.sh
```

else, you can use make -j<your host cpu cores> instead

## install from docker image

use below command to download offical docker image from docker hub

```shell
docker pull armoniax/amnod
```

