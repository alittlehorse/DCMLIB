# DCMLIB

# log:
2018/06/03

- 修复了OB,OW,OF的GetString解码问题

2018/06/04

- 增加了解码DICOM文件(.dcm)的功能

2018/06/07

- 统一了DicomDictionary接口,消去了中间变量Tag
- 修改了OB解码中Int8的BUG
- 增加了WriteValue<T>和ReadValue<T>的模板方法

2018/06/12
- 增加了图像处理功能

2018/06/26
- 增加了更换预设窗位的功能

2020/04/14
- 加入项目说明和致谢
  
# 简介：
DICOM：医学数字成像和通信标准(Digital Imagingand Communication of Medicine, DICOM)，是美国放射学会(American College ofRadiology， ACR)和美国电器制造商协会(National Electrical Manufacturers Association， NEMA)组织制定的专门用于医学图像的存储和传输的标准

本项目是造轮子项目  
1.  实现DICOM二进制信息的编码与解码
2.  实现DICOM二进制医学图像文件，即.dcm文件得解码与显示

## DICOM的语法和语义
DICOM定义自己的“语法”和“词汇”，解决二义性问题  
其中标记“**Tag**”就是词汇,用数据字典给出详细的定义和解释，另外用唯一标识符（**UID**）的方法给出唯一标识  
而“语法”就是信息组成规则,比如大端传输还是小端传输，显式VR还是隐式VR

### 语义问题：

UID：
```
例子：
1.2.840.10008.5.1.4.1.1.2 表示CT图像储存
```
Tag:
```
(0008,0008) 表示图像类型
```
那么将Tag和UID结合在一起是不是可以表示这个图片是CT图像了呢？就像c语言中变量名和变量值一样？
```
(0008,0008)1.2.840.10008.5.1.4.1.1.2 
表示CT图像吗？
```
c语言中定义变量名时会确定变量的**类型**和**长度**，就像**Int类型**是**4**字节，**char**类型是**1**字节。DICOM的二进制信息中也应该定义类型和长度。

DICOM采用了TLV模式，即Tag + VR+ Length + Value
```
VR是表示法，表示这个值是Int、Date、Time、String、浮点、结构体等类型  
lenght 表示最后的Value占用了多少个字节，
```
这样，就像c语言的变量名和变量值一样，DICOM的语义问题解决了

![image1](https://github.com/alittlehorse/DCMLIB/blob/master/Introduction%20image/%E6%95%88%E6%9E%9C%E5%9B%BE.png)
### 语法问题：
传输语法定义了三个方面的内容：
```
值表示法(VR):显式VR、 隐式VR  
字节顺序： Little Endian、 Big Endian  
压缩格式： JPEG/RLE/有损/无损  
```
具体见DICOM文档，这里给出一个例子，

***Little Endian ,显示VR***传输语法：

**10 00 10 00 4E 50 0C 00 00 00 43 4F 54 54 41 5E 41 4E 4E 41 4C 20**

表示为  
**Tag:(0001,0001)**  
**VR:为（50 4E）,解码后PN 病人姓名**  
**Length为0000000C,长为12**   
**值为：（43 4F 54 54 41 5E 41 4E 4E 41 4C 20）COTTA^ANNAL**  

解码完毕。

以上是一个非常简单的解码过程，在深入DICOM协议的过程中你还会发现非常复杂的编码规则，比如length不确定，留有保留位，**结构体嵌套**等，较为繁琐，请多多查询DICOM文档，再对应阅读源码

![image2](https://github.com/alittlehorse/DCMLIB/tree/master/Introduction%20image/效果图.png)

# 备注：
测试图片为\DCMLIB\bin\Debug\dicom.dcm

# 致谢：
感谢郑建立老师的辛勤教诲，和耐心地解答。郑老师是我见过地最认真负责的老师，在此向郑老师表达由衷的敬意！


