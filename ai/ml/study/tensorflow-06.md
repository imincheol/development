# Softmax Classification 

https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-06-1-softmax_classifier.py

Linear regression -> Logistic Classification -> Softmax Classification 

## Softmax function 

Scores ---[Softmax]---> Probabilities 

  hypothesis = tf.nn.softmax( tf.matmul(X,W)+b ) 

## Cost function  : cross entropy 

  Y - log(\hat{Y})

## One-Hot encoding 

tf.argmax

```
// softmax
a = sess.run(hypothesis, feed_dict={X: [[1, 11, 7, 9]]})

// one-hot encoding
print(a, sess.run(tf.argmax(a, 1)))
```





# Fancy Softmax classification 

https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-06-2-softmax_zoo_classifier.py

- cross_entropy
- one_hot
- reshape

## softmax_cross_entropy_with_logits 

Scores ---[Softmax]---> Probabilities 
(logit)

- logits = tf.matmul(X,W) + b
- hypothesis = tf.nn.softmax(logits)

Basic 
  - costs = tf.reduce_mean( -tf.reduce_sum(Y * tf.log(hypothesis), axis=1))

softmax_cross_entropy_with_logits 
  - cost_i = tf.nn.softmax_cross_entropy_with_logits(logits=logits, labels=Y_one_hot)
  - cost = tf.reduce_mean(cost_i)


//
