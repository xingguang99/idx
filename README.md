相关脚本：

export PORT=8080 UUID=自定义
curl -sSL https://raw.githubusercontent.com/vevc/one-node/refs/heads/main/google-idx/install.sh | sh

uuid生成器【点击获取】

重启命令：

app/xray/startup.sh

原作者项目地址【点击查看】

如果节点测试-1：选中节点，编辑配置文件将 Alpn 默认的：http/1.1改成 h2


节点自动保活教程


1. 安装 docker

dev.nix 第 16 行

services.docker.enable = true;

（输入：docker ps 检测是否正常运行）

2. 安装保活脚本

curl -sSL https://raw.githubusercontent.com/vevc/one-node/refs/heads/main/google-idx/keepalive/install.sh | sh

3. 修改 app.js 环境变量

app.js 第 4-11 行

// ============================================================

// Remote
const targetUrl = 'https://8080-firebase-us-1747877258236.cluster-2xfkbshw5rfguuk5qupw267afs.cloudworkstations.dev' 

const ffOpenUrl = 'https://idx.google.com/us-51072006

// Local

const projectDir = '/home/user/tw'   项目名称

const vncPassword = 'vevc.firefox.VNC.pwd'  密码

// ============================================================

输入：pwd 查看路径

4. 设置开机自启

dev.nix onStart 方法

第49行

xray = "/home/user/项目名称/app/xray/startup.sh";
idx = "/home/user/项目名称/app/idx-keepalive/startup.sh";

（输入：docker ps 检测是否正常运行）

dev.nix 配置文件参考：https://github.com/vevc/one-node/blob/main/google-idx/keepalive/dev.nix

5. 首次登录，让浏览器记住用户名密码信息

开放浏览器 5800 端口，通过 VNC 登录 idx

6. 删除容器，触发保活，测试自动登录

docker rm -f idx

7. 检查 idx 自动登录

登录 VNC，查看 idx 空间是否正常打开

验证保活效果
