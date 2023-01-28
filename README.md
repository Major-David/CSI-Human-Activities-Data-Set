# CSI-Human-Activities-Data-Set
CSI Data Set use for Human Activities Recognition and Fall Detection


数据集包含五个受测者在两个不同环境中采集的十一种动作，每个受测者在每个环境中所做的每个动作采集20个数据样本，数据集共有2200个样本。

This dataset contains 11 kinds of activities act by 5 volunteers in two different environment , the data of each activity act by one volunteer in each environment has 20 samples. The number of samples in this dataset is 2200.



## 设备  Device

·发射端和接收端为两台搭载 Intel 5300网卡的PC

We use two PC with Intel 5300 NIC as signal emitter and receiver

·发射速率：20 p/s

Sample rate: 20 packet/second



## 数据格式  Data Format

数据包含十一种活动，数据受测者有5人，测试环境包含卧室和会议室两个环境。

The dataset contains 11 kinds of activities, 5 volunteers and 2 kinds of environment participate in collecting data. The kinds of environments contains bedroom and meeting room.

每一个活动在每个环境中采集100个样本（跌倒活动采集50个样本），其中每个受测者采集20个样本。

Each activity in one environment contains 100 samples (The activity of Fall Down contains 50 samples) , the data of each activity act by one volunteer in each environment has 20 samples. 

#### 动作种类  Activities

1   --  平躺		lying
2   --  坐立		sitting
3   --  跑动		running
4   --  走动		walking
5   --  捡东西	pick up
6   --  挥手		wave hand
7   --  跳跃		jump
8   --  下蹲		squat
9   --  坐下		sit down
10 --  站起		stand up
11 --  跌倒		fall down



#### 原始数据   Original Data

原始数据为接收器收集到的未经处理的数据，数据保存为.dat文件，可以通过Script中的read_bf_file.m进行解析，获取RSSI、CSI等无线信号信息。关于具体的使用可以参考http://dhalperi.github.io/linux-80211n-csitool/faq.html

Original Data is unprocessed data collected by the receiver, each of the data is saved as  .dat  file. The file can be parsed by  read_bf_file.m  in document Script to get RSSI and CSI of wireless signal. The specific method of use can be found in http://dhalperi.github.io/linux-80211n-csitool/faq.html

原始数据中的平躺、坐立动作的每条数据长度为6分钟左右，每个受测者在每个环境中收集1条数据，可根据需要进行切割。其他动作的每条数据长度为15秒左右，动态动作（比如下蹲）动作在整条数据中部位置开始。

The length of each data of the activity lying and sitting is about 6 minutes, we collected 1 sample for each volunteer in each environment. The data can be sliced as needed. The length of other activity data is about 15 seconds, and the dynamic activity start at the middle of the sample.  

**样本：XXX_yy i.dat代表XXX被测者在yy动作的第i条数据**	

Sample:  XXX_yy i.dat  represent the i th	yy activity sample of the volunteer XXX	



#### 处理后数据   Processed Data（建议使用  Recommend to use）

处理后数据通过将原始数据提取、切割、补全等处理，提取CSI信息并统一尺寸。处理后数据每个环境中，每个动作有五个受测者，每个受测者提供20个数据样本。处理后数据的每个数据样本保存为.mat文件，其中保存一个名为 csi 的3 * 30 * 200尺寸（3条发射天线 * 30个子载波 * 200个包即10秒动作数据）复矩阵，复矩阵csi即为提取出的CSI矩阵。

 Processed Data is the Original Data after extracting, slicing, completing. Each of data has the same shape.The data of each activity act by one volunteer in each environment has 20 samples. Each sample is saves as  .mat  file, the file contains a complex matrix named "csi" . The shape of the matrix is 3 * 30 * 200 (3 antennas * 30 subcarrier * 200 packets which means 10 seconds activity data). The matrix is the CSI matrix.

**样本：XXX_yy i.mat代表XXX被测者在yy动作的第i条数据**

Sample:  XXX_yy i.mat  represent the i th	yy activity sample of the volunteer XXX

**ps：处理用到的代码都在Script中，切割平躺、坐立的是OwnData_cut.m ，提取CSI并将数据切割为10秒长的是OwnData_extract.m**
