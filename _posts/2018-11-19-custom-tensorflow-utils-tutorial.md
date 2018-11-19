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

### tf_utils.tensorboard.Tensorboard

Defined in `tensorflow_utils/tensorboard.py`.  

TensorBoard operates by reading TensorFlow events files, which contain summary data that you can generate when running TensorFlow. For more information, see [Serializing the data](https://www.tensorflow.org/guide/summaries_and_tensorboard).  

**\_\_init\_\_**

```ruby
__init__(
    log_dir='checkpoint'
    overwrite=True
)
```

Contstructs a `Tensorboard` instance, which is a suite of visualization tools for TensorFlow training framework (e.g. loss graph, embeddings).

Args:  

- **`log_dir`**: A string containing a directory in which to export timestamped (if available) model and its checkpoint. The sub-directories will be automatically created if not exist.

- **`overwrite`**: An optional bool to overwrite all the previous checkpoint and saved models. 



<br/>

#### Methods

---

**init_scalar**  

```ruby
init_scalar(collections=None)
```

Initializes all scalar values stored in the given collections by attaching `tf.summary.scalar` .  Make sure that the value in any of the collections is scalar type and pre-exists using `tf.add_to_collection()`.  

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

Operations in TensorFlow don't do anything until you run them, or an op that depends on their output. And the summary nodes that we've just created are peripheral to your graph: none of the ops you are currently running depend on them.  

In order to generate summaries, you need to run all of these summary nodes, which means they should hold the value of tensor in the graph. We offer you a simple method managing them (which you have already initialized with `Tensorboard.init_scalar()`) by using [`tf.summary.merge_all`](https://www.tensorflow.org/api_docs/python/tf/summary/merge_all). 

Args:  

- **`sess`**: A TensorFlow `Session` object.
- **`feed_dict`**:  A dictionary that maps graph elements to values. (must be compatible feed values for the respective elements of keys)



<br/>

**display_summary**

```ruby
display_summary(time_stamp=False)
```

Initializes all scalar values stored in the given collections by attaching `tf.summary.scalar` .  Make sure that the value in any of the collections is scalar type and pre-exists using `tf.add_to_collection()`.  

The summary variables in the given collections will be identified by the name of their collection.  

Args:  

- **`log_dir`**: A string containing a directory in which to export timestamped (if available) model and its checkpoint. The sub-directories will be automatically created if not exist.
- **`overwrite`**: An optional bool to overwrite all the previous checkpoint and saved models. 

Raises:

- **`ValueError`**: Could not find a `value` in `collections`.   

---



### Images: Image Processing and Decoding Operations

Defined in `tensorflow_utils/images.py`

<br/>

**tf_utils.images.batch_wavelet_tranform**

```ruby
tf_utils.images.batch_wavelet_tranform(
    images,
    wavelet='haar',
    recon=False
)
```
Args:  
- **`images`**: 4-D Array of shape `[batch, height, width, channels]`. Note that only gray scale `images` is currently available (channels=1).
- **`wavelet`**: Wavelet to use.
- **`recon`**: An optional bool. Default to false performing 2D single-level wavelet decomposition. If true, `images` with 4 different frequency details are reconstructed by inverse transformatation.

Return:
- If `recon` was false, 4-D Array of shape `[batch, height/2, width/2, 4]`, else 4-D Array of shape `[batch, height*2, width*2, 1]`.

Raises:
- **`ValueError`**: If the shape of `images` is incompatible with the shape arguments to this function.
- **`ValueError`**: If the channel of `images` is greater than 1 such as RGB.  

<br/>

**tf_utils.images.linear_windowing_from_dicom**
```ruby
tf_utils.images.linear_windowing_from_dicom(
    dicom_info
)
```
Args: 
- **`dicom_info`**: The metadata of DICOM file, containing pixel arrays and windowing components.

Return:
- 2-D linear windowed image of shape `[height, width]`.

Raises:
- **`ValueError`**: If `dicom_info` has neither `window level` or `window width`.

- **`ValueError`**: If not pixel ranging flag `MONOCHROME1` and `MONOCHROME2` exist in `dicom_info`. 


<br/>

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})

Further Information: <dongyul.oh@snu.ac.kr>

<br/>

