Tensor flow install Mac
https://www.tensorflow.org/install/install_mac

#1 Install Python 3
Python 3.6.5 
https://www.python.org/downloads/release/python-365/

#2 Tensorflow Installing with Virtualenv 
https://www.tensorflow.org/install/install_mac#installing_with_virtualenv

```
$ sudo easy_install pip
$ sudo pip install --upgrade virtualenv 
$ virtualenv --system-site-packages -p python3 ~/tensorflow
$ cd ~/tensorflow
$ source ./bin/activate

(tensorflow)$ easy_install -U pip
(tensorflow)$ pip3 install --upgrade tensorflow

```

#3 Check tensorflwo 

```
$ python3 
>>> imnport tensorflwo as tf 
>>> tf.__version__
$
```
'1.8.0'

#4 Hello world 
```
>>> hello = tf.constant("Hello, TensorFlow!")
>>> sess = tf.Session()
```
b'Hello, TensorFlow!'
