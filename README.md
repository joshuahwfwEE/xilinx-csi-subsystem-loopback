# xilinx-csi-subsystem-loopback
this project is based on xilinx dphy loopback repository, this repos will focus on how the controller interact with DPHY lane module and PPI protocol  
tuser[95:0]:  

bit[0]: sof    
bit[32:1]: mipi datatype  
bit[47:33]:  
bit[63:48]: word count  
bit[95:64]:  

mipi datatype:  

1.Data Type Description: 0x00 to 0x17  
0x00 to 0x07 Synchronization Short Packet Data Types    
0x08 to 0x0F Generic Short Packet Data Types    
0x10 to 0x17 Generic Long Packet Data Types    

2.Data Type Description: 0x18 to 0x1F YUV Data    
0x18 YUV420 8-bit    
0x19 YUV420 10-bit    
0x1A Legacy YUV420 8-bit    
0x1B Reserved    
0x1C YUV420 8-bit (Chroma Shifted Pixel Sampling)    
0x1D YUV420 10-bit (Chroma Shifted Pixel Sampling)    
0x1E YUV422 8-bit    
0x1F YUV422 10-bit     

Data Type Description: 0x20 to 0x27 RGB Data    
0x24 to RGB888 Data    
 


Data Type Description: 0x28 to 0x2F RAW Data   
0x28 RAW6  
0x29 RAW7  
0x2A RAW8  
0x2B RAW10  
0x2C RAW12  
0x2D RAW14  
0x2E RAW16  
0x2F Reserved    


Data Type Description: user defined    
0x30 to 0x37 User Defined Byte-based Data  
0x38 to 0x3F Reserved  

word count:  
Because the MIPI CSI-2 TX Subsystem is transmitting video line-data as a single long packet, WC can be calculated as follows:    
WC = (pixel number per-line) x (bit per-pixel) / 8  

Please see the following WC calculation examples for different cases:  

a) 1000 pixel, RAW8:  
  
    WC=1000 pixel x 8 bit /8 = 1000 bytes = 0x03E8  
  
b) 1000 pixel, RAW10:  
  
    WC=1000 pixel x 10 bit /8 = 1250 bytes = 0x04E2  
  
c) 1000 pixel, RAW12:  
  
    WC=1000 pixel x 12 bit /8 = 1500 bytes =  0x05DC  
      
d) 1920 pixel RGB888:    
  
    WC=1920 pixel x 24 bit /8 = 5760 bytes =  0x1680    
     
d) 1920 pixel YUV422:    
  
    WC=1920 pixel x 8 bit /8 = 1920 bytes =  0x780    

example1:
vpg datawidth: [24:0]  
rgb888 1L, 1PPC data width [47:0], burst rate: 124.5Mhz =1920x1080x60   
Pixel Encoding for Single Pixel per Beat with C_CSI_MAX_BPC =14:  
tdata[7:0],6'b000000,  //G0[13:6]  
tdata[15:8],6'b000000, //B0[27:20]   
tdata[23:16],6'b000000,//R0[41:34]  
6'b000000  

example2:
vpg datawidth: [24:0]  
yuv422 4L, 1PPC data width [47:0], burst rate: 124.5Mhz =1920x1080x60   
Pixel Encoding for Single Pixel per Beat with C_CSI_MAX_BPC =14:  
tdata[7:0],6'b000000,  //Y0/Y1[13:6]    
tdata[15:8],6'b000000, //U0/V0[27:20]   
tdata[23:16],6'b000000,//R0[41:34]  
6'b000000  

example3:
vpg datawidth: [47:0]  
yuv422 4L, 2PPC data width [87:0], burst rate: 148.5Mhz =2200x1125x60    
Pixel Encoding for dual Pixel per Beat with C_CSI_MAX_BPC =14:  
tdata[7:0],6'b000000,  //Y0[13:6]    
tdata[15:8],6'b000000, //U0[27:20]   
tdata[23:16],6'b000000,//Y1[41:34]  
tdata[31:24],6'b000000,//V0[55:48]
32'b0

example4:
vpg datawidth: [95:0]  
yuv422 4L, 4PPC data width [167:0], burst rate: 200Mhz = 32x64x97656.25  
Pixel encoding for Quad Pixel per Beat with C_CSI_MAX_BPC =14:  
tdata[7:0],6'b000000    //Y0[13:6]    
tdata[15:8],6'b000000,  //U0[27:20]       
tdata[23:16],6'b000000, //Y1[41:34]    
tdata[31:24],6'b000000, //V0[55:48]    
tdata[39:32],6'b000000, //Y2[69:62]  
tdata[47:40],6'b000000, //U2[83:76]  
tdata[55:48],6'b000000, //Y3[97:90]  
tdata[63:56],6'b000000, //V2[111:104]  
56'b0
  
this repos conatin 2 project:  
  
1. csi rgb888 loopback test  
2. csi raw14 loopback test  

