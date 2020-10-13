# espui

### 简介
ESPUI是一个简单、友好的ESP32/ESP8266配网工具，让ESP8266配网就像配置家用路由器一样简单方便。

### Issue
- 加载速度慢，受限于ESP8266性能，整个后台页面首次加载需要5s甚至更久，同时希望能够找到更简单的UI框架，能够让后台更快的加载。
- 待优化

### 使用
`````cpp
//写完了就放代码
#include <stdint.h>
#include <string.h>
#include <ESP8266WiFi.h>
#include <ArduinoJson.h>

#include "src/espui.h"

Espui espui;

void OnLog(String log)
{
    if (!Serial)
    {
        return;
    }
    Serial.println(log);
}

void SerialPrint(String log)
{
    //build time string
    int time_length = 13;
    long time = micros() / 1000;
    String time_str = String(time);
    String time_str_padding = "";
    int padding_length = time_length - time_str.length();
    for (int i = 0; i < padding_length; i++)
    {
        time_str_padding += "0";
    }
    time_str_padding += time_str;
    String log_content = "[" + time_str_padding + "][Info]" + log;
    OnLog(log_content);
}

void setup()
{
    Serial.begin(115200);

    espui.SetLogger(OnLog);
    if (espui.Begin())
    {
        SerialPrint("Load successful.");
    }
    else
    {
        SerialPrint("Load failed.");
    }
}

void loop()
{
    // put your main code here, to run repeatedly:
    espui.Loop();
}

`````

### 函数
- Begin
参数：无
返回值：bool
简介：启动WIFI连接或开启AP模式。

- Loop
参数：无
返回值：void
简介：loop.

### 引用

- [ArduinoJson](https://github.com/bblanchon/ArduinoJson "ArduinoJson")

### 捐赠
![捐赠 支付宝](https://github.com/withsalt/espui/blob/main/documents/alipay.jpg "捐赠 支付宝" )

### Stargazers over time
[![Stargazers over time](https://starchart.cc/withsalt/BilibiliLiveTools.svg)](https://starchart.cc/withsalt/BilibiliLiveTools)
