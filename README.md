# camera
**使用V4L2获取摄像头的JPEG照片，用720P的摄像头进行的测试 产品型号：WQ-Z10A006V1**

## 编译
1. 自定义宏 `WIDTH HEIGHT DEVICE_NAME`决定分辨率的宽和高，和v4l2设备名字.
2. `arm-fsl-linux-gnueabi-gcc test_v4l2.c -static` 并将生成的执行文件`copy`到`android`系统的`/bin`目录下.
3. 可以用gcc直接编译，运行在本地linux系统中.
 
## 运行
1. `./a.out` 将会产生10张照片在当前目录下，名字为`picture0-picture9`.

## 问题
1. 会出现`<3>uvcvideo: Failed to resubmit video URB (-27).`经过查询`-27`的含义为 `-27：EFBIG		27	/* File too large */` 我理解为usb带宽不够导致。

## 解决
* 将触摸屏的usb断开，问题解决。 

## 结论
1. 可以直接采集JPEG图片，只可通过修改其分辨率和色度来改变文件的大小。

|分辨率  	|文件大小|
|-----------|-------|
|1280*960	|2.63M	|
|640*480	|900K	|
|320*240	|225K	|

## 总结
1. urb发送失败，根据提示为文件太大了，考虑为带宽不够。
2. 遇上这种情况应考虑usb供电不足。应将其它usb设备移除单独测试usb摄像头。

