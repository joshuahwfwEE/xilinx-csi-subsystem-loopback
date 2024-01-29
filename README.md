# xilinx-csi-subsystem-loopback
this project is based on xilinx dphy loopback repository, this repos will focus on how the controller interact with DPHY lane module and PPI protocol  
mipi datatype:  

Data Type Description
0x00 to 0x07 Synchronization Short Packet Data Types
0x08 to 0x0F Generic Short Packet Data Types
0x10 to 0x17 Generic Long Packet Data Types
0x18 to 0x1F YUV Data
0x20 to 0x27 RGB Data
0x28 to 0x2F RAW Data
0x30 to 0x37 User Defined Byte-based Data
0x38 to 0x3F Reserved

Data Type Description
0x28 RAW6
0x29 RAW7
0x2A RAW8
0x2B RAW10
0x2C RAW12
0x2D RAW14
0x2E RAW16
0x2F Reserved
0x3

Data Type Description
0x18 YUV420 8-bit
0x19 YUV420 10-bit
0x1A Legacy YUV420 8-bit
0x1B Reserved
0x1C YUV420 8-bit (Chroma Shifted Pixel Sampling)
0x1D YUV420 10-bit (Chroma Shifted Pixel Sampling)
0x1E YUV422 8-bit
0x1F YUV422 10-bit  


this repos conatin 2 project:

1. csi rgb888 loopback test  
2. csi raw14 loopback test  

