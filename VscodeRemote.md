# 使用Vscode远程开发

[视频教程](https://www.bilibili.com/video/BV1np4y1B7S7)

【安装 OpenSSH】

` Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'`



` Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0`

 【生成公钥】 `ssh-keygen.exe`

* 一路回车
* 在显示的路径中找到生成文件

