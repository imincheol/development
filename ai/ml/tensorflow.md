Tensor flow install Mac
https://www.tensorflow.org/install/install_mac

## 1 Install Python 3
Python 3.6.5 
https://www.python.org/downloads/release/python-365/

## 2 Tensorflow Installing with Virtualenv 
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

## 3 Check tensorflwo 

```
$ python3 
>>> imnport tensorflwo as tf 
>>> tf.__version__
$
```
'1.8.0'

## 4 Hello world 
```
>>> hello = tf.constant("Hello, TensorFlow!")
>>> sess = tf.Session()
```
b'Hello, TensorFlow!'

## 5 Computational Graph 
```
>>> node1 = tf.constant(3.0, tf.float32)
>>> node2 = tf.constant(4.0)
>>> node3 = tf.add(node1, node2)

>>> print("node1:", node1, "node2:", node2)
node1: Tensor("Const_1:0", shape=(), dtype=float32) node2: Tensor("Const_2:0", shape=(), dtype=float32)

>>> print("node3:", node3)
node3: Tensor("Add:0", shape=(), dtype=float32)

>>> print("sess.run(node1, node2): ", sess.run([node1, node2]))
sess.run(node1, node2):  [3.0, 4.0]

>>> print("sess.run(node3): ", sess.run(node3))
sess.run(node3):  7.0

```

## 6 Placeholder
```
>>> a = tf.placeholder(tf.float32)
>>> b = tf.placeholder(tf.float32)
>>> adder_node = a + b

>>> print(sess.run(adder_node, feed_dict={a: 3, b: 4.5}))
7.5

>>> print(sess.run(adder_node, feed_dict={a: [1,3], b: [2, 4]}))
[3. 7.]
```

