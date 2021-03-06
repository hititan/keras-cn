# utils 工具

本模块提供了一系列有用工具


##CustomObjectScope
```python
keras.utils.generic_utils.CustomObjectScope()
```
提供定制类的作用域，在该作用域内全局定制类能够被更改，但在作用域结束后将回到初始状态。
以```with```声明开头的代码将能够通过名字访问定制类的实例，在with的作用范围，这些定制类的变动将一直持续，在with作用域结束后，全局定制类的实例将回归其在with作用域前的状态。

```python
with CustomObjectScope({"MyObject":MyObject}):
    layer = Dense(..., W_regularizer="MyObject")
    # save, load, etc. will recognize custom object by name
```

## HDF5Matrix

```python
keras.utils.io_utils.HDF5Matrix(datapath, dataset, start=0, end=None, normalizer=None)
```

这是一个使用HDF5数据集代替Numpy数组的方法

提供```start```和```end```参数可以进行切片，另外，还可以提供一个正规化函数或匿名函数，该函数将会在每片数据检索时自动调用。

```python
x_data = HDF5Matrix('input/file.hdf5', 'data')
model.predict(x_data)
```

* datapath: 字符串，HDF5文件的路径
* dataset: 字符串，在datapath路径下HDF5数据库名字
* start: 整数，想要的数据切片起点
* end: 整数，想要的数据切片终点
* normalizer: 在每个切片数据检索时自动调用的函数对象


## to_categorical
```python
to_categorical(y, num_classes=None)
```

将类别向量(从0到nb_classes的整数向量)映射为二值类别矩阵, 用于应用到以`categorical_crossentropy`为目标函数的模型中.

###参数

* y: 类别向量
* num_classes:总共类别数

## normalize
```python
normalize(x, axis=-1, order=2)
```

对numpy数组规范化，返回规范化后的数组

###参数
* x：待规范化的数据
* axis: 规范化的轴
* order：规范化方法，如2为L2范数


## convert_all_kernels_in_model
```python
convert_all_kernels_in_model(model)
```

将模型中全部卷积核在Theano和TensorFlow模式中切换

### plot_model
```python
plot_model(model, to_file='model.png', show_shapes=False, show_layer_names=True)
```
绘制模型图

### custom_object_scope
```python
custom_object_scope()
```
提供定制类的作用域，在该作用域内全局定制类能够被更改，但在作用域结束后将回到初始状态。
以```with```声明开头的代码将能够通过名字访问定制类的实例，在with的作用范围，这些定制类的变动将一直持续，在with作用域结束后，全局定制类的实例将回归其在with作用域前的状态。

本函数返回```CustomObjectScope```对象

```python
with custom_object_scope({"MyObject":MyObject}):
	layer = Dense(..., W_regularizer="MyObject")
	# save, load, etc. will recognize custom object by name
```

### get_custom_objects
```python
get_custom_objects()
```

检索全局定制类，推荐利用custom_object_scope更新和清理定制对象，但```get_custom_objects```可被直接用于访问```_GLOBAL_CUSTOM_OBJECTS```。本函数返回从名称到类别映射的全局字典。

```python
get_custom_objects().clear()
get_custom_objects()["MyObject"] = MyObject
```

### serialize_keras_object
```python
serialize_keras_object(instance)
```
将keras对象序列化

### deserialize_keras_object
```python
eserialize_keras_object(identifier, module_objects=None, custom_objects=None, printable_module_name='object')
```
从序列中恢复keras对象

### get_file

```python
get_file(fname, origin, untar=False, md5_hash=None, cache_subdir='datasets')
```

从给定的URL中下载文件, 可以传递MD5值用于数据校验(下载后或已经缓存的数据均可)

### 参数

* fname: 文件名

* origin: 文件的URL地址

* untar: 布尔值,是否要进行解压

* md5_hash: MD5哈希值,用于数据校验

* cache_subdir: 用于缓存数据的文件夹

### 返回值

下载后的文件地址
