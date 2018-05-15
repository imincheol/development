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

- python4 
- tensorflow

```
$ python3 
>>> import tensorflow as tf 
>>> tf.__version__
'1.8.0'
```


## 4 Hello world 

- tf.constant
- tf.Session

```
>>> hello = tf.constant("Hello, TensorFlow!")
>>> sess = tf.Session()
```
b'Hello, TensorFlow!'

## 5 Computational Graph 

- tf.add
- print 
- sess.run

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

- tf.placeholder
- sess.run(op, feed_dict={x: data})

```
>>> a = tf.placeholder(tf.float32)
>>> b = tf.placeholder(tf.float32)
>>> adder_node = a + b

>>> print(sess.run(adder_node, feed_dict={a: 3, b: 4.5}))
7.5

>>> print(sess.run(adder_node, feed_dict={a: [1,3], b: [2, 4]}))
[3. 7.]
```

## 7 Tensor

Everything is Tensor 

- Tensor
  - Ranks 
  - Shapes 
  - Types 
 
- Rank 

| Rank | Math entity           | Python example  |
| :--: |-------------------------------| -----|
| 0    | Scalar (magnitude only)         | s = 486 |
| 1    | Vector (magnitude and direction)| v = [1.0, 2.1, 3.2] |
| 2    | Matrix (table of numbers)       | m = [[1,2,3], [4,5,6], [7,8,9]] |
| 3    | 3-Tensor (cube of numbers)      | t = [[[2], [4], [6]], [[1],[3],[5]], [[3],[8],[9]]]  |
| n    | n-Tensor                        | .... |

- Shape

| Rank | Shape               | Demension number |
| :--: |:-------------------:| :----------------:|
| 0    | []                  | 0-D              |
| 1    | [D0]                | 1-D              |
| 2    | [D0, D1]            | 2-D              |
| 3    | [D0, D1, D2]        | 3-D              |
| n    | [D0, D1, ..., Dn-1] | n-D              |

- Types 
  - tf.float32
  - tf.int32


