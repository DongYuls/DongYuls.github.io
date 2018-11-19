---
layout: post
title:  "Custom Tensorflow Utilities Reference Guide"
date:   2018-11-19 12:56:10 +0700
categories: [Tensorflow, Custom Utility, Reference]
---

---

Last Modified: 2018.11.19

This is my custom library (tensorflow wrapper) documentation. All the classes and functions introduced in this article are basically implemented by TensorFlow to support deep learning researcher.

---

### Tensorboard: Visualizing Learning

<br/>

#### tf_utils.tensorboard.Tensorboard

Defined in `tensorflow_utils/tensorboard.py`.  

TensorBoard operates by reading TensorFlow events files, which contain summary data that you can generate when running TensorFlow. For more information, see [Serializing the data](https://www.tensorflow.org/guide/summaries_and_tensorboard).  

**\_\_init\_\_**

```ruby
__init__(
    log_dir='checkpoint'
    overwrite=True
)
```

Contstructs a `Tensorboard` instance visualizing TensorFlow training framework (e.g. loss graph, embeddings). 

Args:  

- **`log_dir`**: A string containing a directory in which to export timestamped (if available) model and its checkpoint. The sub-directories will be automatically created if not exist.

- **`overwrite`**: An optional bool to overwrite all the previous checkpoint and saved models. 

<br/>

**init_scalar**  

```ruby
init_scalar(collections=None)
```

Initializes all scalar values stored in the given collections by attaching `tf.summary.scalar` .  The value in any of the collections must be scalar type and pre-exist through `tf.add_to_collection()`.  

The summary variables in the given collections will be identified by the name of their collection.  

Args:  

- **`collections`**: Collection list containing the summary variables to be saved. 


<br/>

**init_images**

```ruby
init_scalar(
    collections=None,
    num_outputs=1
)
```

The summary has up to `num_outputs` summary values containing images. The images are built from `tensor` which must be 4-D with shape `[batch_size, height, width, channels]` and where `channels` can be:

- 1: `tensor` is interpreted as Grayscale.
- 3: `tensor` is interpreted as RGB.
- 4: `tensor` is interpreted as RGBA.

The images have the same number of channels as the input tensor. For float input, the values are normalized one image at a time to fit in the range `[0, 255]`. `uint8` values are unchanged. The op uses two different normalization algorithms:

- If the input values are all positive, they are rescaled so the largest one is 255.
- If any input value is negative, the values are shifted so input value 0.0 is at 127. They are then rescaled so that either the smallest value is 0, or the largest one is 255.

For further details on this `tf.summary.images` operations , check out the docs on [here](https://www.tensorflow.org/api_docs/python/tf/summary/image).

Args:  

- **`collections`**: Collection list containing the summary variables to be saved.
- **`num_outputs`**: Max number of batch elements to generate images for. 

<br/>

**add_summary**

```ruby
add_summary(
    sess,
    feed_dict,
    log_type='train'
)
```

In order to generate summaries, you need to run all of these summary nodes, which means they should hold the value of tensor in the graph. We offer you a simple method managing them (which you have already initialized above) by using [`tf.summary.merge_all`](https://www.tensorflow.org/api_docs/python/tf/summary/merge_all). 

Args:  

- **`sess`**: A TensorFlow `Session` object.
- **`feed_dict`**:  A dictionary that maps graph elements to values. (must be compatible feed values for the respective elements of keys)

<br/>

**display_summary**

```ruby
display_summary(time_stamp=False)
```

Displays summaries (e.g. global step, loss, accuracy) in the console.

Args:  

- **`time_stamp`**: An optional bool to log time (time elapsed between the training steps). 

---

<br/>

#### Example Code:

The following code demonstrates a single training step and validation loop for a large scale of dataset or possibly other dataset that needs a loop to compute the evaluation metrics. Note that here training and validation loops are sharing two variables, `loss_curr` and `accuracy_curr`, to add summaries to their own logs.

```python
import tensorflow as tf
import tensorflow_utils as tf_utils

images = tf.placeholder(tf.float32, shape=[None, 299, 299, 3])
labels = tf.placeholder(tf.int32, shape=[None, 10]) # one-hot encoded labels

logits = ... # the output of your model

loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(labels=labels, logits=logits))
accuracy = tf.reduce_mean(tf.equal(tf.argmax(logits, 1), tf.argmax(labels, 1)))

tensorboard = tf_utils.Tensorboard(log_dir='checkpoint')

# summary variables to temporarily store the corresponding values
loss_curr = tf.get_variable(name='Loss', shape=[], trainable=False, initializer=tf.zeros_initializer())
accuracy_curr = tf.get_variable(name='Acc', shape=[], trainable=False, initializer=tf.zeros_initializer())

tf.add_to_collection('tensorboard', loss_curr)
tf.add_to_collection('tensorboard', accuracy_curr)
tensorboard.init_scalar(collections=['tensorboard'])

sess = tf.Session()

train_images, train_labels = ...

# compute loss and accuracy of training batch
values = sess.run([model.loss, model.accuracy], feed_dict={images: train_images, labels: train_labels})
# add summaries to training logs
tensorboard.add_summary(sess=sess, feed_dict=[loss_curr: values[0], acc_curr: values[1]], log_type='train')

# validation step
test_loss, test_acc = [], []
while True:
    try: test_images, test_label = ... 
    except: break
        
    values = sess.run([loss, accuracy], feed_dict={images: test_images, labels: test_labels})
    test_loss.append(values[0])
    test_acc.append(values[1])

# add summaries to validation/test logs
tensorboard.add_summary(sess=sess, feed_dict={loss_curr: np.mean(test_loss), acc_curr: np.mean(test_acc)}, log_type='test')

tensorboard.display_summary(time_stamp=False)
```

To launch tensorboard after training, use the following command: `tensorboard --logdir=checkpoint`.

<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

Further Information: <dongyul.oh@snu.ac.kr>

<br/>

