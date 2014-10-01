#Butterflow

*Butterflow* is an easy to use command line tool that lets you create fluid slow
motion and smooth motion videos.

#####How does it work?

It works by generating intermediate frames between existing frames. For example,
given two existing frames `A` and `B`, this program can generate frames `C.1`,
`C.2`...`C.n` that are positioned between the two. This process, called
[motion interpolation](http://en.wikipedia.org/wiki/Motion_interpolation),
increases frame rates and can give the perception of smoother motion and more
fluid animation, an effect most people know as the "soap opera effect".
Butterflow takes advantage of this increase in frame rates to generate high fps
videos that are needed to make smooth and slow motion videos with minimal
judder.

#####See it for yourself:

* [Video @30fps slowed down with butterflow (210fps)](https://dl.dropboxusercontent.com/u/103239050/INK-SIDE.mp4)
* [Video @12fps frame rate increased with butterflow (96fps)](https://dl.dropboxusercontent.com/u/103239050/GEL-SIDE.mp4)

##Installation

####On Ubuntu:

1. `$ apt-add-repository ppa:dthpham/butterflow`
2. `$ apt-get update`
3. `$ apt-get install butterflow`

If you need [`ffmpeg`]():

1. `$ apt-add-repository ppa:jon-severinsson/ffmpeg`
2. `$ apt-get update`
3. `$ apt-get install ffmpeg`

####On Arch Linux:

A package is available in the AUR under [butterflow](https://aur.archlinux.org/packages/butterflow/).

####With pip:

1. Satisfy all the dependencies
2. `$ pip2 install butterflow`

####From Source:

1. Satisfy all the dependencies
2. Clone this repository or download a [source package](https://github.com/dthpham/butterflow/releases).
3. `$ python2 setup.py init`
4. `$ python2 setup.py develop`
5. `$ python2 setup.py test`
6. `$ python2 setup.py install`

##Dependencies

Installing these aren't necessary if you installed using a package.

####On Ubuntu, Debian:

* [`git`]()
* [`build-essential`]()
* [`pkg-config`]()
* [`ffmpeg`]()
* [`python-dev`]()
* [`python-setuptools`]()
* [`python-numpy`]()
* [`python-opencv`]()
* [`opencl-headers`]()
* [`libopencv-dev (>=2.4.8)`]()
* [`libopencv-ocl-dev`]()
* [`mesa-common-dev`]()
* [`ocl-icd-libopencl1`]()

####On Arch Linux:

* [`git`]()
* [`libcl`]()
* [`ffmpeg (>=2.4.1)`]()
* [`opencv (>=2.4.9)`]()
* [`python2-numpy`]()

##Setup

After installing the package, you still need to install ***at least one***
vendor-specific implementation of OpenCL that matches your hardware:

####On Ubuntu:

* [`nvidia-opencl-icd-304-updates`]()
* [`nvidia-opencl-icd-331-updates`]()
* [`beignet`]()

####On Debian:

* [`nvidia-opencl-icd`]()
* [`amd-opencl-icd`]()
* [`amd-opencl-icd-legacy`]()
* [`mesa-opencl-icd`]()
* [`beignet`]()

####On Arch Linux:

* [`opencl-nvidia`](https://developer.nvidia.com/opencl)
* [`opencl-nvidia-304xx`]()
* [`intel-opencl-sdk`](https://software.intel.com/en-us/intel-opencl)
* [`intel-opencl-runtime`]()
* [`amdapp-sdk`](http://developer.amd.com/tools-and-sdks/opencl-zone/)
* [`opencl-mesa`](http://www.x.org/wiki/GalliumStatus/)
* [`beignet`](http://cgit.freedesktop.org/beignet/)

For more information on how to satisfy the OpenCL requirements, please read
[this page](http://wiki.tiker.net/OpenCLHowTo). If you're on Arch Linux, see
[this page](https://wiki.archlinux.org/index.php/Opencl).

##Usage

For a full list of options run ```$ butterflow -h```.

####Increase a video's frame rate to `120fps`:

```
$ butterflow <video> --playback-rate 120
```

####Slow-mo a clip with a target frame rate of `400fps`:

```
$ butterflow <video> --playback-rate 59.94 -t full,fps=400
```

####Slow-mo a clip to `0.25x` quarter speed:

```
$ butterflow <video> --playback-rate 59.94 -t full,factor=0.25
```

####Slow-mo a clip to be `30s` long:

```
$ butterflow <video> --playback-rate 59.94 -t full,duration=30
```

####Slow-mo a region:

```
$ butterflow <video> --playback-rate 24 -t \
a=00:00:05.0,b=00:00:06.0,factor=0.5
```

####Slow-mo multiple regions:

```
$ butterflow <video> --playback-rate 24 -t \
"a=00:00:05.0,b=00:00:06.0,fps=200;\
a=00:00:16.0,b=00:00:18.0,fps=400;\
a=00:00:18.0,b=00:00:20.0,factor=0.5"
```

##Filters

####Decimate:

Videos may have some judder if your source has duplicate frames. To compensate
for this, use the `--decimate` option:

```
$ butterflow <video> --playback-rate 60 --decimate
```

####Video Scale:

To scale the output video to `75%` of its original size:

```
$ butterflow <video> --playback-rate 24 --video-scale 0.75
```
