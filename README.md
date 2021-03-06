# sdk使用说明

> 文件夹及文件说明：

> Agora-Android-Tutorial-1to1-ASR 文件夹是语音识别demo

> Agora-Android-Tutorial-1to1-EVAL文件夹是语音评测demo

> unisound libs文件夹下是云知声jar包，jar包同时支持识别和评测能力

> asr.apk是编译好的识别demo，eval.apk是编译好的评测demo，demo使用时需要两个手机，由于token 24小时失效，运行前需要修改token

## 一、环境准备

> 1.把工程导入Android studio；

> 2.项目依赖

```
implementation 'com.squareup.okhttp3:okhttp:3.10.0'

implementation 'com.alibaba:fastjson:1.2.73'
```

> 3.项目权限

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

> 4.修改配置

> 修改app\src\main\res\values文件夹下面strings.xml 相应的asr_app_key、asr_app_secret和eval_app_key

> 评测的eval_app_key传入方式是AppKey@AppSecret形式 ，例如注册用户后创建的的应用信息如下：

> 那么输入的评测的eval_app_key传入方式是appkey@AppSecret形式

## 二、项目sdk使用说明

> sdk包为unisound.jar

### 调用实时识别

```
 a. 调用AsrWebsocket.getInstance().init进行初始化需要传入appkey 和 secret，可选参数为识别地址；
 b. AsrWebsocket.getInstance().start开始识别，需要传入AsrResultListener实例，此实例为识别结果和错误结果回调
    参数AsrParam ，此参数为识别配置参数，可选参数为布尔类型是否使用本地录音，true为使用本地录音，如果需要上传音频文件或者数据流，此参数传false，
    然后调用AsrWebsocket.getInstance().send(audioData, 0, audioData.length)传音频
 c. AsrWebsocket.getInstance().stop();结束识别
 
``` 
### 调用语音评测

```
 a. 调用EvalWebsocket.getInstance().init进行初始化，可选参数为评测地址；
 b. EvalWebsocket.getInstance().start开始评测，需要传入EvalResultListener实例，此实例为评测结果和错误结果回调，
    参数EvalParam，此参数为评测配置参数，可选参数为布尔类型是否使用本地录音，true为使用本地录音，如果需要上传音频文件或者数据流，此参数传false
    然后调用EvalWebsocket.getInstance().send(audioData, 0, audioData.length)传音频
 c. EvalWebsocket.getInstance().stop();结束评测
```
