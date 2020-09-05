方案说明 
1、一键脚本需要VPS安装为CentOS7系统
2、本方案需要一个域名并解析到你的VPS的IP，随便买个一刀以内的便宜域名，freenom可能不好申请免费的域名了。
3、编译安装支持TLS1.3的nginx，安装过程稍慢，耐心等待
4、当前版本v2ray不支持TLS1.3，当v2ray支持后，本次一键搭建的服务端可升级支持
5、搭配bbr加速，可以让速度有较大的提升
6、一键脚本会为你配置一个英文模板的网站，你也可以自行替换自己的网页。

一、一键脚本搭建服务端 1、使用SSH工具连接VPS，执行下列命令，选择安装v2ray+ws+tls
curl -O https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls.sh && chmod +x v2ray_ws_tls.sh && ./v2ray_ws_tls.sh 2、等待脚本执行，过程中会提示需要输入域名，输入解析到本VPS的域名，然后回车
3、等待安装完成，你可以看到配置参数，客户端配置时用到。
4、安装BBR加速（可不安装，或自行开启bbr），下面命令，分享自网络
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh 5、注意在弹出的安装界面首先选择1，安装BBR内核,安装过程可能时间较长,耐心等待。
6、安装完成后会提示重启VPS,输入Y，然后回车，确认重启。然后等待几分钟，再使用xshell连接vps（连接方法是点软件上打开，找到之前保存的连接，然后点连接）登陆后执行下列命令
cd /usr/src && ./tcp.sh 7、在弹出安装界面,输入5,然后回车，使用BBR魔改版加速，等待安装完成提示bbr启动成功即可。

二、fork A大的v2ray-ws-tls 一键脚本
使用方法 1、系统要求：centos7
2、使用以下命令，安装wordpress+v2ray_ws_tls1.3，因为nginx是编译安装，脚本会稍慢一些。
yum install -y wget && wget https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls_with_wp.sh && chmod +x v2ray_ws_tls_with_wp.sh && ./v2ray_ws_tls_with_wp.sh 3、安装完成后，访问域名，开始进入wordpress初始配置页面，自行配置即可。
4、安装完成后，会显示v2ray配置参数，手动填写到v2ray客户端中即可。若忘记了，使用以下命令查看参数
cat /etc/v2ray/myconfig.json 5、建议搭配BBR使用，速度更快，分享一下网上的BBR一键脚本，先安装内核，重启后再次执行脚本安装加速。
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

三、wordpress+v2ray_ws_tls1.3一键脚本，同时安装wordpress和v2ray，兼具建站和代理
一点建议 1、不要用配置低的VPS玩这一套方案，卡死没商量
2、因为nginx的安装是编译安装，所以速度会比较慢
3、如果ssh连接不稳定可能会中断安装，如果有此情况，建议使用screen命令，具体用法请谷歌
使用方法 1、系统要求：centos7
2、使用以下命令，安装wordpress+v2ray_ws_tls1.3，因为nginx是编译安装，脚本会稍慢一些。
yum install -y wget && wget https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls_with_wp.sh && chmod +x v2ray_ws_tls_with_wp.sh && ./v2ray_ws_tls_with_wp.sh 3、安装完成后，访问域名，开始进入wordpress初始配置页面，自行配置即可。
4、安装完成后，会显示v2ray配置参数，手动填写到v2ray客户端中即可。若忘记了，使用以下命令查看参数
cat /etc/v2ray/myconfig.json 5、建议搭配BBR使用，速度更快，分享一下网上的BBR一键脚本，先安装内核，重启后再次执行脚本安装加速。
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

四、vless+ws+tls1.3一键脚本（2020.08.28） 讲解如何配置前，先放个一键脚本，修复了很久之前的v2ray+ws+tls1.3脚本，之前因为官方安装脚本更新无法使用，目前已正常使用。同时copy了一份稍微修改了一下配置文件，改为vless+ws+tls1.3的一键脚本，目前已测试centos7/ubuntu18.04/debian10均可以正常使用。
bash <(curl -L -s https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/v2ray_ws_tls1.3_vless.sh)
vless+ws+tls配置文件 这里贴一下server的配置文件和nginx配置文件，客户端配置文件可直接在v2rayN等工具中手动填写使用或导出。注意：配置文件中的注释需要全部删掉。
vless+ws+tls模式下，nginx是前置的，根据访问路径分流访问流量，只有路径匹配的会转发到v2ray，此种模式可以套CDN。


vless+ws+tls1.3一键脚本
vless + ws + tls1.3一键脚本，搭建简单
此模式可以套CDN（执行一键脚本时不要开启CDN）
此模式使用nginx ws中转，相比vless+tcp+tls，多了一层ws，开销多一点
目前已测试centos7/ubuntu18.04/debian10均可以正常使用
未知问题请反馈https://t.me/atrandys
先放个一键脚本，修复了很久之前的v2ray+ws+tls1.3脚本，之前因为官方安装脚本更新无法使用，目前已正常使用。同时copy了一份稍微修改了一下配置文件，改为vless+ws+tls1.3的一键脚本，目前已测试centos7/ubuntu18.04/debian10均可以正常使用。

bash <(curl -L -s https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/vless_ws_tls.sh)

vless+tcp+tls一键脚本
vless + tcp + tls一键脚本，搭建也简单，已配置好fallbacks
此模式不可以套CDN
目前已测试centos7/ubuntu18.04/debian10均可以正常使用
未知问题请反馈https://t.me/atrandys
bash <(curl -L -s https://raw.githubusercontent.com/atrandys/v2ray-ws-tls/master/vless_tcp_tls.sh)
