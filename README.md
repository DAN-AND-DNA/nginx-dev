# 安装nginx开发环境（代码跳转、vscode、能断点）
希望代码跳转、可视化并且能断点
1. 从官方下载nginx代码 https://nginx.org/en/download.html
2. 安装nginx依赖，并编译:
    ```bash
    sudo apt-get install libz-dev libpcre3-dev libssl-dev build-essential
    ./configure --prefix=xxxx
    make
    make install
    ```
3. 下载vscode，安装：
    ```bash
    dpkg -i xxxxx
    ```
4. 复制配置到.vscode目录下：
```json
// launch.json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
        "name": "(gdb)Launch",
        "type": "cppdbg",
        "request": "launch",
        "program": "${workspaceFolder}/objs/nginx",
        "args": ["-c", "${workspaceFolder}/conf/nginx.conf"],
        "stopAtEntry": true,
        "cwd": "${workspaceFolder}",
        "environment": [],
        "externalConsole": false,
        "MIMode": "gdb",
        "preLaunchTask": "Compile"
    }]
}


// tasks.json
{
    "version": "2.0.0",
    "tasks": [{
        "label": "Compile",
        "command": "make",
        "args": [],
        "type": "shell",
        "group": {
            "kind": "build",
            "isDefault": true
        },
        "presentation": {
            "echo": true,
            "reveal": "always",
            "focus": false,
            "panel": "new",
        },
        "problemMatcher":"$gcc",
    }]
}

```
5. nginx-1.16.1/conf/nginx.conf 改如下：
```nginx
master_process off;
worker_processes  1;
daemon off;


http {
    server {
        listen       8080;
    }
}
```
6. 打开vscode下载c/c++插件，可以进行调试或者查看代码了 ：)
