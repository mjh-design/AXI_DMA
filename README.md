# AXI_DMA_CONTROLLER
## Block Diagram  
![image](https://user-images.githubusercontent.com/71507230/195854675-7dc040a5-a50e-4d52-b9fd-0b9ffeac3024.png)
## Signal and Interface Pins
|Name|Type|Description|
|---|---|---|
|AXI_ACLK|Clock|All signals and are synchronous to this clock.| 
rtl代码采用Xilinx风格编写。  
本设计可将DMA接收到的读写大块数据的命令拆分成多个burst发送，只有第一个burst需要处理4k边界问题。  
数据位宽设为32位，由于仿真器不支持太大的mem，将地址设为16位，一次burst传输最多传输1kB数据。
读通道的master支持outstanding，slave有支持outstanding和不支持两个版本，如果例化的是不支持的版本，读通道也会像写通道一样读完一个burst再发下一个请求。
tb向DMA的读写通道发同样的命令，同时读写同一块区域。
没有用到AXI协议的CACHE,lOCK,和QOS信号。
