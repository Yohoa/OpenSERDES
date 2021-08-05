# OpenSERDES

Serializer/Deserializer (**SerDes**) is the most important functional block used in high speed communication.

串行器/解串器 (**SerDes**) 是高速通信中最重要的功能块。

SerDes converts parallel data into a serial (one bit) stream of data that is transmitted over a high-speed connection, such as LVDS, to a receiver that converts the serial stream back to the original, parallel data. 

SerDes 将并行数据转换为串行（一位）数据流，该数据流通过高速连接（例如 LVDS）传输到接收器，该接收器将串行流转换回原始的并行数据。

A global CLOCK signal is present to sequence the serialization and deserialization of data from one block to another.

存在全局时钟信号CLOCK，以对从一个块到另一个块的数据的串行化和逆串行化变换。

![Test Image 1](https://github.com/SparcLab/OpenSERDES/blob/master/Serdes_Overview.png)


Technology: **Skywater OpenPDK 130nm**

Tools Used: **OpenLane, Virtuoso Cadence**

The **Serializer** and **Deserializer** blocks are coded in Verilog HDL and synthesized using Openlane tool mapped to Sky130 CMOS technology. Simulation results and associated gds, spice and netlist files are uploaded in Serializer and Deserializer folders respectively

串行器和解串器模块以 Verilog HDL 编码，并使用映射到 Sky130 CMOS 技术的 Openlane 工具进行合成。仿真结果和相关的 gds、spice 和网表文件分别上传到 Serializer 和 Deserializer 文件夹中

A chain of CMOS inverters is used as TX driver to drive the input capacitance of the channel. The gds, spice, netlist and. oa files for the same are present in **Inverter_Based_Tx** folder

一串 CMOS 反相器用作发送端TX驱动器来驱动通道的输入电容。 gds、spice、网表和。 **Inverter_Based_Tx** 文件夹中保存对应的 oa 文件

A fully synthesizable Rx is designed using Resistive FB inverter followed by CMOS inverter as sensing and gain element respectively. The following DFF is used to sample the data using the clock recovered by the CDR.

一个完全可综合的 Rx 设计使用电阻 FB 反相器（Resistive FB inverter），最后信号进入CMOS 反相器，分别作为传感和增益元件。随后的 DFF 使用 CDR 恢复的时钟信号来对数据进行采样。

**Resistive Feedback inverter** is used as sensing element to sense low amplitude received signal at the front end of the receiver. Details of the implementation of Resistive FB inverter can be found in Resistive_FB_inverter folder

**电阻反馈反相器**（Resistive Feedback inverter）用作感应元件，用于感应接收器前端的低幅度接收信号。 Resistive_FB_inverter 文件夹中可以找到 Resistive FB 逆变器的实现细节

DFF is the simplest memory block to sample and store the data before deserializing. Master Slave DFF is implemented using NAND logic gates. Details of the same are present in **DFF** and **NAND** folders

DFF 是最简单的内存块，用于在反序列化之前对数据进行采样和存储。主从 DFF 是使用 NAND 逻辑门实现的。 **DFF** 和 **NAND** 文件夹中存在相同的详细信息

**Oversampling CDR** is used to recover the data and clock from the received signal. The CDR uses the data transitions to tune the clock frequency for proper decoding of received signal. The **Oversampling_CDR** folder contains the gds, spice and synthesized Verilog files generated from Openlane tool.

**过采样CDR**用于从接收到的信号中恢复数据和时钟。CDR 使用数据转换来调整时钟频率，以便正确解码接收信号。 **Oversampling_CDR** 文件夹包含从 Openlane 工具生成的 gds、spice 和合成 Verilog 文件。

