# x-ui

Support multi-protocol multi-user XRAY panel
# Features

- System status monitoring
- Support multi-user multi-protocol, web page visualization operation
- Support protocol：vmess、vless、trojan、shadowsocks、dokodemo-door、socks、http
- Support for configuring more transport configurations
- Traffic statistics, restricting traffic, limit expiration time
- Can customize XRAY configuration template
- Support HTTPS access panel (self -reserve domain name + SSL certificate)
- Support the one -click SSL certificate application and automatically renew the visa
- More advanced configuration items, details

# Installation & upgrade

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

## Manual installation & upgrade

1. First download the latest compression pack from https://github.com/vaxilu/x-ui/releases, generally select the `amd64` architecture
2. 

> If your server CPU architecture is not `AMD64`, replace the` amd64` in the command to other architecture replace `amd64` in the command with another architecture

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Use docker installation

> This docker tutorial and Docker mirror are provided by [chasing66] (https://github.com/chasing66)

1. Install docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Install x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build Your own imageown image

```shell
docker build -t x-ui .
```

## SSL certificate application

> This function and tutorial are provided by [FranzkafKayu] (https://github.com/franzkafkkay)

The script built-in SSL certificate application function, using this script application certificate, needs to meet the following conditions:

- Knowing Cloudflare registered mailboxese registered mailboxes
- Know the Cloudflare Global API KeyAPI Key
- The domain name has been parsed to the current server through Cloudflareparsed to the current server through Cloudflare

How to get Cloudflare Global API Key:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

When you use it, you only need to enter the `domain name`,` mail`, `API Key`, the schematic diagram is as follows:
        ![](media/2022-04-04_141259.png)

Precautions:

-TThis script uses DNS API to apply for a certificateS API to apply for a certificate
-Use Let'sencrypt as a CA side by default
-Certificate installation directory is /root/cert directory
-This script application certificate is a pan-domain name certificate

## TG robot use (in development, not available for the time being)

> This function and tutorial are provided by [FranzkafKayu] (https://github.com/franzkafkkay)

X-UI supports daily traffic notifications, panel login reminders and other functions through TG robots. Using TG robots, you need to apply by yourself
For specific application tutorials, please refer to [Blog Link](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions for use: Set robot -related parameters in the background
- TG robot token
- TG robot Chatid
- TG robot cycle running time, use Crontab syntax  

Reference grammar:
- 30 * * * * * //Notification of each point 30s
- @hourly      //Notice per hour
- @daily       //Notice every day (at 0:00 in the morning)
- @every 8h    //Notice every 8 hours  

TG notification content:
-In node traffic use
-The panel login reminder
-On node reminder
-Catal warning reminder

More functional planning ...

## Suggestion system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# common problem

## Move from V2-UI

First install the latest version of the X-UI on the V2-UI server, and then use the following command to migrate to migrate this machine V2-UI `All inbound account data` to x-ui，`Panel settings and username passwords will not migrate`

> After the migration is successful, please turn off the v2-ui` and restart the X-UI`, otherwise the inbound of V2-UI will have the `port conflict with the inbound of X-UI.

```
x-ui v2-ui
```

## issue closure

Various small white problems can see high blood pressure

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
