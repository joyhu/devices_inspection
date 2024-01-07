﻿# 简介

- 工作中经常需要对客户的网络设备进行巡检，之前都是用SecureCRT开启记录Log Session，依次远程登录到每个设备上，依次输入巡检命令收集设备巡检信息；

- 现在希望利用Python能够实现自动登录设备，自动抓取巡检信息，并且使用多线程技术，缩减巡检时间；

- 在登录出现故障时，能够记录Log提醒工程师稍后手动排查故障再进行巡检。

- 使用脚本能够在脚本所在目录下生成当前日期的巡检信息存放目录，其中每个设备的巡检信息文件以主机名称命名。

- .py脚本已经封装为.exe程序，配合info文件，可以方便的在没有Python环境的PC上使用。（可在Releases中下载）

# 使用方法

- 脚本移植请利用requirements.txt文件，使用下面的命令安装所需的第三方库。

```python
pip install -r requirements.txt
```

- 准备info.xlsx文件，与.py脚本存放于同一目录，文件里应存有需要巡检的设备登录信息和巡检命令。

info文件内sheet1存放网络环境中被巡检的设备登录信息，如下：
![20-38-18](https://github.com/icefire-ken/Devices_Inspection/assets/26742041/e5e78532-52ee-4e76-bcd6-14b5031294c5)

info文件内sheet2存放网络设备巡检输入的命令，如下：
![20-39-41](https://github.com/icefire-ken/Devices_Inspection/assets/26742041/7eba04d7-38ff-4baa-9650-5e4c6d0aea72)

- 使用下面的命令运行脚本，开始巡检。

```python
python devices_inspection.py
```

- 也可以使用.exe可执行程序，开始巡检。

![20-48-52](https://github.com/icefire-ken/Devices_Inspection/assets/26742041/99edaca6-27b3-4ebd-88ed-7799b04a5a3d)

## 关于info文件中的Secret密码！

- 如果人工登录设备没有要求输入Enable Password，info文件中的Secret字段为空（无需填写）。
- A10设备默认是没有Enable Password的，但进入Enable模式时，仍然会提示要求输入Enable Password，人工操作时可以直接Enter进入；使用脚本时需要在info文件的Secret字段中填入空格即可。

# 更新日志

## 2023.12.28

- info文件添加了部分锐捷类型设备的巡检命令。

## 2023.12.25

- 为了方便在没有Python环境的PC上使用，以将.py脚本打包成了.exe程序。
- EXE程序Release，想要直接使用的朋友可以在Releases下载EXE程序，配合info文件使用。

## 2023.06.19

- 修复了巡检命令输入等待结果时间过长的问题，大幅缩短巡检时间。
  
## 2022.11.07

- 修复了CMD窗口内巡检过程实时显示，有可能发生的多个设备信息在同一行显示的问题。

## 2022.08.12

- A10设备请注意，若Enable密码为空，则需要在info文件中的Secret列中填补空格，否则会报“登录信息错误”异常。

## 2022.06.21

- 增加了对Telnet连接超时的异常捕获，并记录到日志文件中。

## 2021.12.28

- 为项目添加requirements.txt文件，方便脚本移植。

## 2021.12.13

- 修复多线程对01log文件操作时可能出现的冲突问题。
- 修复保存的巡检文件和log文件打开时会出现乱码的问题。

## 2021.12.02

- 修复读取设备登录信息中的纯数字内容为数字类型，不能供给Netmiko使用的问题。

## 2021.11.04

- 为info文件添加需要使用telnet登录的标识。
- 为“设备管理地址不可达！”登录异常修改描述“设备管理地址或端口不可达！”。
- info文件添加了部分华三（hp_comware）类型设备的巡检命令。

## 2021.11.01

- 加入登录设备出现错误信息的记录功能，会在巡检目录下创建01log文件来记录设备登录时出现的异常。
- info文件添加了部分Cisco ASA（cisco_asa）类型设备的巡检命令。
- 修复读取巡检命令时，由于pandas出现的nan。

## 2021.10.02

- 为避免过多消耗设备性能，加入巡检最大线程限制，默认最大100个线程。
- info文件添加了部分华为（huawei）类型设备的巡检命令。

## 2021.09.17

- 初次上传脚本。
- 脚本已经实现基本功能，及多线程巡检功能。
- info文件中Sheet2只包含了cisco_ios、a10的巡检命令。
