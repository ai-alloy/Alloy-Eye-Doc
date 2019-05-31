进入build目录下执行./getbin.sh xxx；xxx指代src下的项目名称，比如项目名称是hello_world

执行./getbin.sh hello_world

![](/images/complier-start.png)

在build目录会生成hello_world目录，包含最终生成的hello_world.bin固件，此固件是最终下载到开发板上的。

![](/images/complier-end.png)

注意：getbin.sh脚本第7行/opt/my-kendryte-toolchain是编译工具默认路径，此路径必须和编译工具实际放置的位置一致。

![](/images/get-sh.png)

