环境&使用：
    需要组播源或替换为其他来源
    centos6.9
    cd stream_pusher/build; cmake ../; make; ./stream_pusher 

功能：
    ffmpeg拿到组播数据推rtsp/rtmp音视频流到服务器，支持H264, AAC-LC；

实现：
    1、通过注册ffmpeg数据读取回调函数直接从内存读取数据推流，此种方法需要设置输出帧率等于输入源的帧率，否则音视频不同步。
       同时若源视频帧率改变则音视频也无法同步；
    2、通过直接填充ffmpeg的AVpack结构体来实现推流，此种方法无需设置帧率，源帧率改变后音视频依旧能保持同步，但是时间戳需要我们自己处理；