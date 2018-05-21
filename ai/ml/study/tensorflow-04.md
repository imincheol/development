
# Multi-Variable Linear Regression 

Hypothesis using matrix 

## 1 Basic 

```
x1_data = [73., 93., 89., 96., 73.]
x2_data = [80., 88., 91., 98., 66.]
x3_data = [75., 93., 90., 100., 70.]

y_data = [152., 185., 180., 196., 142.]

# placeholders for a tensor that will be always fed.
x1 = tf.placeholder(tf.float32)
x2 = tf.placeholder(tf.float32)
x3 = tf.placeholder(tf.float32)

Y = tf.placeholder(tf.float32)

w1 = tf.Variable(tf.random_normal([1]), name='weight1')
w2 = tf.Variable(tf.random_normal([1]), name='weight2')
w3 = tf.Variable(tf.random_normal([1]), name='weight3')
b = tf.Variable(tf.random_normal([1]), name='bias')

hypothesis = x1 * w1 + x2 * w2 + x3 * w3 + b
```

Too many lines
Complicatied

## 2 Matrix 

```

x_data = [[73., 80., 75.],
          [93., 88., 93.],
          [89., 91., 90.],
          [96., 98., 100.],
          [73., 66., 70.]]
y_data = [[152.],
          [185.],
          [180.],
          [196.],
          [142.]]


# placeholders for a tensor that will be always fed.
X = tf.placeholder(tf.float32, shape=[None, 3])
Y = tf.placeholder(tf.float32, shape=[None, 1])

W = tf.Variable(tf.random_normal([3, 1]), name='weight')
b = tf.Variable(tf.random_normal([1]), name='bias')

# Hypothesis
hypothesis = tf.matmul(X, W) + b
```
* Placeholder 
  * X = tf.plcaeholder(tf.float32, shape=[None, 3])
  * Y = tf.plcaeholder(tf.float32, shape=[None, 1])

## 3 Loading Data from File

### Data File 
  * csv 

data-01-text-scroe.csv

```
# EXAM1,EXAM2,EXAM3,FINAL
73,80,75,152
93,88,93,185
89,91,90,180
96,98,100,196
```

### Load Data File 

```
import numpy as np

xy = np.loadtxt('data-01-test-score.csv', delimiter=',', dtype=np.float32)

x_data = xy[:, 0:-1]
y_data = xy[:, [-1]]
```

* Same data type 

### numpy

Slicing data 

```
nums = range(5)

print nums        # [0, 1, 2, 3, 4]
print nums[:]     # [0, 1, 2, 3, 4]

print nums[2:4]   # [2, 3]

print nums[2:]    # [2, 3, 4]
print nums[:2]    # [0, 1]

print nums[:-1]   # [0, 1, 2, 3]
```

## Queue Runners 

### Step
  * Filenames -> [Random Shuffle] 
  * -> Filename Queue -> [Reader] -> [Decoder] 
  * -> Example Queue 

```
# 1 Filenames 
filename_queue = tf.train.string_input_producer(
    ['data-01-test-score.csv'], shuffle=False, name='filename_queue')

# 2 File Reader 
reader = tf.TextLineReader()
key, value = reader.read(filename_queue)

# 3 Parsing (Decode)
record_defaults = [[0.], [0.], [0.], [0.]]
xy = tf.decode_csv(value, record_defaults=record_defaults)

```

### Batch 

* tf.train.batch

```
# collect batches of csv in
train_x_batch, train_y_batch = \
    tf.train.batch([xy[0:-1], xy[-1:]], batch_size=10)
```

* Coordinator 
```
# Start populating the filename queue.
coord = tf.train.Coordinator()
threads = tf.train.start_queue_runners(sess=sess, coord=coord)

# Session run

# End 
coord.request_stop()
coord.join(threads)
```

//
