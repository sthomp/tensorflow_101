# Tensorflow 101
Playing around with tensorflow and neural nets

## Running tensorflow via docker

Install docker on OSX:

```
brew install docker-machine
brew install docker
```

Run a docker machine:

```
docker-machine start default
```

Run the container interactively and mount a host directory (in this case making a new workspace called `tensorflow_dev`. For docker to mount a directory in osx it must be under `/Users/`):

```
docker run -it --name tensorflow --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow
```

Run the container 1 off

```
docker run --name tensorflow --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow /bin/sh -c 'cd tensorflow_dev && python mnist.py'
```

If the container has network connectivity issues try running with `--net=host`

Other docker commands:

```
cd tensorflow_dev
python mnist.py

docker start tensorflow

docker attach tensorflow

docker rm -v tensorflow
```
