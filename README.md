# AudioTransform_AAC

使用ffmpeg，将任意格式的音频数据转化为AAC格式的音频数据


- 通过输入音频地址，创建音频转化器

```objectivec
    ZSJTranscode_AAC *tranc = [[ZSJTranscode_AAC alloc]initWithInputPath:fileName outputBlock:nil];
```

- 设置输出数据回调


```objectivec
    __weak ZSJTranscode_AAC *weakTranc = tranc;
    tranc.outputBlock = ^(NSData* data, NSTimeInterval pts , NSInteger size) {
        
        if (data) {
            [fileHandle writeData:[weakTranc adtsHeader:data.length]];
            [fileHandle writeData:data];
        }
    };
```

-  读取数据

```objectivec
    while (!tranc.isFinish) {
        [tranc readData]; //没调用一次，读取一帧aac数据
    }

```





