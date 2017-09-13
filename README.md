# docker-xdebug
[使用vscode远程调试docker容器内的php应用](http://xdxd.love/2017/09/13/%E4%BD%BF%E7%94%A8vscode%E8%BF%9C%E7%A8%8B%E8%B0%83%E8%AF%95docker%E5%AE%B9%E5%99%A8%E5%86%85%E7%9A%84php%E5%BA%94%E7%94%A8/)

经常使用docker搭建各种环境进行漏洞测试。如何调试docker内的代码的也成为了一个新需求。使用xdebug插件，可以方便的调试docker内的php应用。



## docker环境安装xdebug

已经整合成docker-compose环境。可以直接clone [github.com/stayliv3/docker-xdebug](https://github.com/stayliv3/docker-xdebug)。

修改xdebug.ini文件内的xdebug.remote_host=172.16.1.203  ip为vscode的机器IP(docker宿主机ip)。


## vscode 配置

vscode安装PHP Debug Adapter for Visual Studio Code。

配置文件为：

    {
        "version": "0.2.0",
        "configurations": [
            
            {
                "name": "Listen for XDebug",
                "type": "php",
                "request": "launch",
                "port": 9000,
                // "stopOnEntry": 1, 运行开始断点，用于调试。
                "serverSourceRoot": "/var/www/html/",
                "localSourceRoot": "/Users/xxxxx/security/coding/xdebug-docker/app"
            },
            {
                "name": "Launch currently open script",
                "type": "php",
                "request": "launch",
                "program": "${file}",
                "cwd": "${fileDirname}",
                "port": 9000
            }
        ]
    }


主要是配置serverSourceRoot和localSourceRoot两个路径。localSourceRoot为vscode看到的php文件路径。然后就可以设置断点，使用vscode进行调试了。

![](/images/dockerdebug1.png)




