# Tensorflow 101
Playing around with tensorflow and neural nets

## Running tensorflow via docker

Install docker on OSX:

```
brew install docker-machine
brew install docker
```

Create a docker machine:

```
docker-machine create --driver virtualbox --virtualbox-memory 8192 --virtualbox-cpu-count 4 default
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

## Image Recognition via Docker

Run default image recognition one off

```bash
docker run --name tensorflow --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow:latest-devel /bin/sh -c 'python /tensorflow/tensorflow/models/image/imagenet/classify_image.py'
```

Run image recognition on your own image one off

```bash
docker run --name tensorflow --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow:latest-devel /bin/sh -c 'python /tensorflow/tensorflow/models/image/imagenet/classify_image.py --image_file /tensorflow_dev/IMG_20151213_171152.jpg'
```

Image Recognition Interactive

```bash
docker run -it --name tensorflow -p 6006:6006 --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow:latest-devel
python /tensorflow/tensorflow/models/image/imagenet/classify_image.py --image_file /tensorflow_dev/IMG_20151213_171152.jpg
```

C++ setup

```bash
docker run -it --name tensorflow -p 6006:6006 --rm -v /Users/scott/Code/web/tensorflow_dev:/tensorflow_dev b.gcr.io/tensorflow/tensorflow:latest-devel

curl -o /tensorflow/tensorflow/examples/label_image/data/inception_dec_2015.zip https://storage.googleapis.com/download.tensorflow.org/models/inception_dec_2015.zip

unzip /tensorflow/tensorflow/examples/label_image/data/inception_dec_2015.zip -d /tensorflow/tensorflow/examples/label_image/data/

cd /tensorflow && bazel build tensorflow/examples/label_image

cd /tensorflow && bazel-bin/tensorflow/examples/label_image/label_image

cd /tensorflow && bazel-bin/tensorflow/examples/label_image/label_image --image=/tensorflow_dev/IMG_20151214_132804.jpg
```


