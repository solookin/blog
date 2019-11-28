#Windows下git换行符配置

为了最大限度兼容macOS,windows以及Linux，需要：

提交时转换为LF，检出时不转换
拒绝提交包含混合换行符的文件

```
git config --global core.autocrlf input
git config --global core.safecrlf true
```
