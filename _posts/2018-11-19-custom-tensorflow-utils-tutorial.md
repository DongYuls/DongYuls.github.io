---
layout: post
title:  "Custom Tensorflow Utilities Reference Guide"
date:   2018-11-19 12:56:10 +0700
categories: [Tensorflow, Custom Utility, Reference]
---

---

Last Modified: 2018.11.07

This is my custom library (tensorflow wrapper) documentation. All the classes and functions introduced in this article are basically implemented by TensorFlow to support deep learning researcher. 

---

### Tensorboard: Visualizing Learning

Defined in `tensorflow_utils/tensorboard.py`

<br/>

#### tf_utils.tensorboard.Tensorboard

TensorBoard operates by reading TensorFlow events files, which contain summary data that you can generate when running TensorFlow. For more information, see [Serializing the data](https://www.tensorflow.org/guide/summaries_and_tensorboard).  

---



#### \_\_init\_\_

---

```ruby
__init__(
    log_dir='checkpoint'
    overwrite=True
)
```

Contstructs an `Tensorboard` instance, which is a suite of visualization tools for Tensorflow training framework (e.g. loss graph, embeddings).

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

Initializes all `value` stored in the given collections by attaching `tf.summary.scalar` .  Make sure that the `value` in any of the collections pre-exists using `tf.add_to_collection()`.  

The summary variables in the given collections will be identified by the name of their collection.  

Args:  

- **`log_dir`**: A string containing a directory in which to export timestamped (if available) model and its checkpoint. The sub-directories will be automatically created if not exist.
- **`overwrite`**: An optional bool to overwrite all the previous checkpoint and saved models. 

Raises:

- **`ValueError`**: Could not find a `value` in `collections`. 

<br/>

**init_images**



**add_summary**

```ruby
add_summary(
    sess,
    feed_dict,
    log_type='train'
)
```





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

