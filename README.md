# DCMLIB
Dicom解码器:

2018/06/03

- 修复了OB,OW,OF的GetString解码问题

2018/06/04

- 增加了解码DICOM文件(.dcm)的功能

2018/06/07

- 统一了DicomDictionary接口,消去了,中间变量Tag,改正了OB解码中Int8的BUG,增加了WriteValue<T>和ReadValue<T>的末班方法