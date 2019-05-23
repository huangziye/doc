

<div style="text-align:center;font-size:30px;font-weight:bold;">IFAA接入说明文档</div>

<br />

<div style="text-align:center;font-weight:bold;">（Android 版本）</div>


<br />
<br />


<table style="width:100%; border-collapse: collapse; text-align: center;">
	<tr style="height:35px">
	  <th style="text-align:center;">时间</th>
	  <th style="text-align:center;">版本</th>
	  <th style="text-align:center;">描述</th>
	  <th style="text-align:center;">作者</th>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;">2019/4/8</td>
	  <td style="text-align:center;">1.0.5</td>
	  <td style="text-align:center;">增加服务接口相关说明</td>
	  <td style="text-align:center;">黄子烨</td>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;">2019/5/6</td>
	  <td style="text-align:center;">2.0.0</td>
	  <td style="text-align:center;">添加SDK直连模式</td>
	  <td style="text-align:center;">黄子烨</td>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	  <td style="text-align:center;"></td>
	</tr>
</table>


<br />
<br />
<br />


# 1. 概述

## 1.1 编写目的

本设计说明文档的编写目的是为了方便接入方快速接入 `IFAA`。


## 1.2 适用范围


本文档适用 Android 端需要接入 `IFAA` 指纹的接入方。



## 1.3 使用


### 1.3.1 引入 `SDK` 包

IFAA SDK 提供了 IFAA 指纹的能力，SDK：


```
// 基础包，测试使用
esand_cloud_core-debug.1.0.0.aar
// 基础包，正式环境使用
esand_cloud_core-release.1.0.0.aar
// 测试环境使用
esand_cloud_ifaa-debug.2.0.0.aar
// 正式环境使用
esand_cloud_ifaa-release.2.0.0.aar
```



### 1.3.2 初始化 `IFAABaseInfo`


在使用 `Android SDK` 前需要初始化 `IFAABaseInfo`。


```
/**
* 初始化数据
*/
private void initIfaaBaseInfo () {
    // app 需要提供给 ifaa 一些基本信息
    ifaaBaseInfo = new IFAABaseInfo (this);
    // TODO 请一定要设定为能够唯一代表自己应用的名字，比如"**银行**手机银行应用"
    // ifaaBaseInfo.setAppName("etasDemo");//在 2.0.0 b版本中去掉了
    // 认证类型，默认为指纹 AUTHTYPE_FINGERPRINT
    ifaaBaseInfo.setAuthType(ifaaAuthType);
    // 业务 ID, 请保持唯一，记录在 ifaa log 中，当出问题时候，查问题用。
    ifaaBaseInfo.setTransactionID(mEtTransactionId.getText().toString());
    // 业务的附加信息，记录在 ifaa log 中，当出问题时，查问题用。
    ifaaBaseInfo.setTransactionPayload(mEtTransactionPayload.getText().toString());
    ifaaBaseInfo.setTransactionType(mEtTransactionType.getText().toString());
    // TODO 用户 id, 此值参与 ifaa 业务以及 token 的生成，务必保证其唯一，可以传入用户名的 hash
    值来脱敏。
    ifaaBaseInfo.setUserID(mEtUserId.getText().toString());
    // 设置使用 SDK 提供的指纹弹框页面
    // reasonTitle、fallbackTitle
    ifaaBaseInfo.usingDefaultAuthUI("EsandDemo","输入密码");
    // 一砂下发的 APPID
    // ifaaBaseInfo.setAppId("xxxxxx");//在 2.0.0 b版本中去掉了
}
```


| 字段 | 类型 | 描述 |
| --- | --- | --- |
| authType | Int | 认证方式 |
| appid | String | 一砂云下发的代表接入方应用身份的appID,,不能为null |
| userId | String | 用户ID或者能够区别用户的唯一表示信息。 |
| transId | String | 能够唯一区别本次IFAA操作的交易ID。此交易ID可以唯一定位此次操作。 |
| transPayload | String | |
| transType | String | 本次IFAA操作的交易类型 |
| reasonTitle | String | 指纹认证弹框页面 title。 |
| fallbackTitle | String | 只有在认证流程中的指纹认证弹框页面，在错误一次的后显示出的可选项按钮标题，如果传入为空，则不显示。 |



### 1.3.3 查询本机是否支持 `IFAA`


`IFAAManager` 中提供了判断当前设备是否支持某种认证类型，现有的认证类型有指纹、人脸，认证类型，详见 `IFAABaseInfo.IFAAAuthTypeEnum` 的枚举。


```
/**
* 是否支持 IFAA
* @param context 执行环境上下文类
* @param authType 认证类型，详见 IFAABaseInfo.IFAAAuthTypeEnum 的枚举
* @return 是否支持 IFAA
*/
public static boolean isSupportIFAA(Context context, IFAABaseInfo.IFAAAuthTypeEnum authType) {}
```


使用该函数：

```
// 检查本机是否支持 IFAA
if (!IFAAManager.isSupportIFAA(this, IFAABaseInfo.IFAAAuthTypeEnum.AUTHTYPE_FINGERPRINT)){
    tvShowInfos.append("此设备不支持 IFAA 指纹");
}
// 其他判断
…
```


### 1.3.4 接入方式一（服务端连接）

#### 1.3.4.1 注册


![注册](images/IFAA_001.png)

<p style="text-align:center;">注册</p>


SDK 对外提供 `com.esandinfo.ifaa.biz.IFAARegister` 类用以实现 IFAA 的注册流程，主要有如下三个函数：


```
// 注册初始化
public IFAAResult regInit()

// 执行注册操作
public void register(String ifaaMsg, IFAACallback IFAACallback)

// 完成注册操作
public IFAAResult regFinish(String ifaaMsg)
```


##### 1.3.4.1.1 注册初始化

```
public IFAAResult regInit()
```


- 入参：无
- 出参：`IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()` 为注册第一次请求需要发送到服务端的报文，其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：


| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_NOT_SUPPORT | 1 | 终端不支持 IFAA（该设备不能使用IFAA指纹或人脸）|
| IFAA_STATUS_NOT_ENROLLED | 4 | 终端没有录入指纹/人脸 (此时可以引导用户去录入指纹/人脸再做操作) |
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|
|IFAA_PERMISSION_DENIED  | 19 | 当前设备未获取相机权限（认证类型为人脸用户没有赋予相机权限） |



##### 1.3.4.1.2 执行注册操作


```
public void register(String ifaaMsg, IFAACallback ifaaCallback)
```

- 入参：
1. `String ifaaMsg`

注册第一次请求服务端返回的报文（客户服务端需要解析此次返回报文，当 `bizContent` 中的 `code` 属性值为`“0000”`时，调用该接口。其他情况按照服务端错误 `code` 列表进行相应的业务处理）

2. `IFAACallback ifaaCallback`


注册操作的回调，该回调中有 2 个实现：`onStatus`、`onResult`。

`onStatus` 返回用户按压指纹返回的各个状态，`onResult` 返回 `IFAAResult`，当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()`
为注册第二次请求需要发送到服务端的报文，其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：

| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （服务器返回报文错误）|
| IFAA_STATUS_RESULT_CANCELED | 12 | 用户取消（APP根据业务自行处理）|
| IFAA_STATUS_RESULT_TIMEOUT | 13 | 本地指纹认证超时（APP提示用户按压指纹）|
| IFAA_STATUS_RESULT_AUTH_FAI | 14 | 验证失败，系统指纹不匹配（APP提示用户按压本地录入的指纹）|
| IFAA_STATUS_RESULT_SYSTEM_BLOCK | 15 | 连续多次校验失败，指纹校验被暂时锁定（各个厂商实现不同，一般1分钟之内可以解锁，继续使用指纹功能）|
| IFAA_STATUS_RESULT_FALLBACK | 16 | 点击了 FALLBACK 按钮（用户点击了指纹弹框上的“输入密码”，APP根据业务自行处理）|
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|
| IFAA_STATUS_RESULT_SYSTEM_ERROR | 18 | 手机系统问题，请升级系统版本|


- 出参：无



##### 1.3.4.1.3 完成注册操作


```
public IFAAResult regFinish(String ifaaMsg)
```

- 入参：`String ifaaMsg`

注册第二次请求服务端返回的报文（客户服务端需要解析此次返回报文，当服务端返回的 `bizContent` 中的
`code` 属性值为`“0000”`时，调用该接口，进行本地完成注册操作。其他情况按照服务端错误 `code` 列表
进行相应的业务处理）

- 出参：`IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，注册成功；其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：

| 常量名 | 值（String） | 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （服务器返回报文错误）|




#### 1.3.4.2 认证



![认证](images/IFAA_002.png)

<p style="text-align:center;">认证</p>


SDK 提供 `com.esandinfo.ifaa.biz.IFAAAuthentication` 实现 IFAA 的认证操作, 主要有如下 2 个函数：


```
// IFAA 认证初始化
public IFAAResult authInit()

// 执行本地认证操作
public void auth(String ifaaMsg, IFAACallback ifaaCallback)
```


##### 1.3.4.2.1 认证初始化


```
public IFAAResult authInit()
```

- 入参：无
- 出参：`IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()` 为认证第一次请求需要发送到服务
端的报文；其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：


| 常量名 | 值（String） | 描述 |
| ---  | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_NOT_SUPPORT | 1 | 终端不支持 IFAA（该设备不能使用IFAA指纹或人脸）|
| IFAA_STATUS_NOT_ENROLLED |4 | 终端没有录入指纹/人脸 (此时可以引导用户去录入指纹/人脸再做操作)|
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|
| IFAA_PERMISSION_DENIED | 19 | 当前设备未获取相机权限（认证类型为人脸用户没有赋予相机权限）|



##### 1.3.4.2.2 认证操作


```
public void auth(String ifaaMsg, IFAACallback ifaaCallback)
```


- 入参：

1. `String ifaaMsg`

认证第一次请求服务端返回的报文（客户服务端需要解析此次返回报文，当服务端返回 `bizContent` 中的
`code` 属性值为`“0000”`时，调用该接口，进行认证操作。其他情况按照服务端错误 `code` 列表进行相应
的业务处理）

2. `IFAACallback ifaaCallback`

认证操作的回调，该回调中有 2 个实现：`onStatus`、`onResult`。

`onStatus` 返回用户按压指纹返回的各个状态，`onResult` 返回 `IFAAResult`，当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()`
为认证第二次请求需要发送到服务端的报文。当收到服务端返回报文时，APP 根据服务端返回 `bizContent`
中的 `code` 值分情况进行处理，当 `code` 为`“0000”`时，认证成功；当 `code` 值为`“2031”`时，进行指位
更新操作，需调用指位更新接口。其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：


| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （服务器返回报文错误）|
| IFAA_STATUS_RESULT_CANCELED | 12 | 用户取消（APP根据业务自行处理）|
| IFAA_STATUS_RESULT_TIMEOUT | 13 | 本地指纹认证超时（APP提示用户按压指纹）|
| IFAA_STATUS_RESULT_AUTH_FAI | 14 | 验证失败，系统指纹不匹配（APP提示用户按压本地录入的指纹）|
| IFAA_STATUS_RESULT_SYSTEM_BLOCK | 15 | 连续多次校验失败，指纹校验被暂时锁定（各个厂商实现不同，一般1分钟之内可以解锁，继续使用指纹功能）|
| IFAA_STATUS_RESULT_FALLBACK | 16 | 点击了 FALLBACK 按钮（用户点击了指纹弹框上的“输入密码”，APP根据业务自行处理）|
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|
| IFAA_STATUS_RESULT_SYSTEM_ERROR | 18 | 手机系统问题，请升级系统版本 |


- 出参：无




#### 1.3.4.3 查询注册状态



![查询注册状态](images/IFAA_003.png)

<p style="text-align:center;">查询注册状态</p>


对外提供 `com.esandinfo.ifaa.biz.IFAAStatus` 类，让用户通过此类的如下接口实现 ifaa 注册状态的查询：


```
// 查询 ifaa 注册状态初始化
public IFAAResult checkStatusInit()

// 查询 ifaa 注册状态
public IFAAResult checkStatus(String msg)
```


##### 1.3.4.3.1 查询 IFAA 注册状态初始化


```
public IFAAResult checkStatusInit()
```


- 入参：无

- 出参：`IFAAResult ifaaResult`


当 `ifaaResult.getCode()` 为 `STATUS_REGISTERED` 时，表示本地取到了 `token`，已经是注册状态，就不发请求到服务端。

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()` 为查询注册状态请求需要发送到服务端的报文；
其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：


| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_REGISTERED | 6 | IFAA 已经注册 (这只是一个状态，并不是错误) |
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|




##### 1.3.4.3.2 查询 IFAA 注册状态




```
public IFAAResult checkStatus(String msg)
```

- 入参：`String ifaaMsg`

查询注册状态请求服务端返回的报文（客户服务端需要解析此次返回报文，当服务端返回 `bizContent` 中的
`code` 属性值为`“0000”`时，调用该接口。其他情况按照服务端错误 `code` 列表进行相应的业务处理）


- 出参：`IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `STATUS_REGISTERED` 时，已经注册；其他的 `ifaaResult.getCode()` 可能出
现的错误码如下表格：



| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_NOT_REGISTERED | 5 | IFAA 尚未注册 (比如认证/注销/指位更新等操作都需要注册后才可以进行) |
| IFAA_STATUS_REGISTERED | 6 | IFAA 已经注册 (这只是一个状态，并不是错误)|
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （此错误发生在服务器）|
| IFAA_STATUS_DELETED | 10 | 本地指纹已经注册，但是注册的指纹模组数据已经被删除（此手机不支持多指位，并且注册的那个指位已经被删除，需要注销后在注册方能使用）|



#### 1.3.4.4 指位更新



SDK 提供了 `com.esandinfo.ifaa.biz.IFAATemplateUpdater` 类实现指位更新操作, 主要有如下函数


```
// 完成指位更新操作
public IFAAResult templateUpdater(String ifaaMessage)
```



##### 1.3.4.4.1 指位更新





![指位更新](images/IFAA_004.png)

<p style="text-align:center;">指位更新</p>


```
public IFAAResult templateUpdater(String ifaaMessage)
```


- 入参：`String ifaaMessage`


当注册第二次请求服务端返回报文 `bizContent` 中 `code` 值为`“2031”`时，调用该接口，接口入参为指纹认
证第二次的请求报文，即 `auth` 方法的回调返回结果对象 `ifaaResult` 的 `msg`(此时 `ifaaResult.code` 为
`IFAA_SUCCESS`）

- 出参：`IFAAResult ifaaResult`


当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()` 为指纹更新请求需要发送到服务端
的报文；客户服务端需要解析指位更新返回报文 `bizContent` 中的 `code` 值为`“0000”`时，指位更新成功。
其他情况按照服务端错误 `code` 列表进行相应的业务处理



#### 1.3.4.5 注销






![注销](images/IFAA_05.png)

<p style="text-align:center;">注销</p>



SDK 提供 `com.esandinfo.ifaa.biz.IFAADeregister` 类进行 IFAA 注销操作，主要有如下函数：


```
// 注销初始化
public IFAAResult deregInit()

// 执行终端注销操作
public void dereg(String ifaaMsg, IFAACallback ifaaCallback)
```



##### 1.3.4.5.1 注销初始化


```
public IFAAResult deregInit()
```

- 入参：无

- 出参：`IFAAResult ifaaResult`


当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，`ifaaResult.getMsg()` 为注册请求发送到服务端的报文；
其他的 `ifaaResult.getCode()` 可能出现的错误码如下表格：


| 常量名 | 值（String）| 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_NOT_SUPPORT | 1 | 终端不支持 IFAA（该设备不能使用IFAA指纹或人脸）|
| IFAA_STATUS_NOT_REGISTERED | 5 | IFAA 尚未注册 (比如认证/注销/指位更新等操作都需要注册后才可以进行) |
| IFAA_STATUS_RESULT_TEE_ ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|



##### 1.3.4.5.2 执行终端注销操作



- 入参：

1. `String ifaaMsg`

注销请求服务端返回的报文（客户服务端需要解析此次返回报文，当服务端返回 `bizContent` 中的 `code` 属
性值为`“0000”`时，调用该接口。其他情况按照服务端错误 `code` 列表进行相应的业务处理）

2. `IFAACallback ifaaCallback`

认证操作的回调，该回调中有 2 个实现：`onStatus`、`onResult`。

此处 `onStatus` 无用，`onResult` 返回 `IFAAResult`，当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，注销成功；其他的 `ifaaResult.getCode()`
可能出现的错误码如下表格：



| 常量名 | 值（String） | 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_CLIENT_ERROR | 8 | 本地执行异常 (错误发生在app执行过程中)|
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （此错误发生在服务器）|


- 出参：无





### 1.3.5 接入方式二（SDK 直连）

为了方便接入方接入 `IFAA` 功能，提供 `SDK` 直接连接 `eDIS` 服务的连接方式。


#### 1.3.5.1 注册


在调用注册前，接入方 APP 需要先请求 APP 服务端获取报文，获取到的报文作为参数传入注册方法中。


```
ifaaManager.reg(msg, new IFAACallback() {}
```

- 入参：

1、接入方 APP 需要先请求 APP 服务端成功返回的报文

2、回调中返回 `IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，注册成功。

- 出参：无





#### 1.3.5.2 认证



```
ifaaManager.auth(msg, new IFAACallback() {})
```


- 入参：

1、接入方 APP 需要先请求 APP 服务端成功返回的报文

2、回调中返回 `IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，再发一次请求到服务到进行确认，发送的报文为 `ifaaResult.getMsg()`。

当 `ifaaResult.getCode()` 为 `IFAA_WRONG_AUTHDATAINDEX` 时，调用指位更新接口，进行指位更新操作。


- 出参：无



#### 1.3.5.3 查询注册状态


```
ifaaManager.checkStatus(msg, new IFAACallback() {})
```


- 入参：

1、接入方 APP 需要先请求 APP 服务端成功返回的报文

2、回调中返回 `IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_STATUS_REGISTERED` 时，已经注册。

- 出参：无



#### 1.3.5.4 指位更新


```
ifaaManager.templateUpdate(msg, new IFAACallback() {})
```


- 入参：

1、接入方 APP 需要先请求 APP 服务端成功返回的报文

2、回调中返回 `IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，再发一次请求到服务到进行确认，发送的报文为 `ifaaResult.getMsg()`. 

- 出参：无




#### 1.3.5.5 注销


```
ifaaManager.unReg(msg, new IFAACallback() {})
```


- 入参：

1、接入方 APP 需要先请求 APP 服务端成功返回的报文

2、回调中返回 `IFAAResult ifaaResult`

当 `ifaaResult.getCode()` 为 `IFAA_SUCCESS` 时，注销成功。


- 出参：无





## 1.4 错误码


### 1.4.1 `IFAAResult` 实体类中的 `code` 值


| 常量名 | 值（String） | 描述 |
| --- | --- | --- |
| IFAA_SUCCESS | 0 | 成功 |
| IFAA_STATUS_NOT_SUPPORT | 1 | 终端不支持 IFAA（该设备不能使用IFAA指纹或人脸）|
| IIFAA_STATUS_FINGERPRINT | 2 | 终端支持IFAA的指纹服务（iOS独有）|
| IIFAA_STATUS_FACE_ID | 3 | 终端支持IFAA的人脸服务（iOS独有）|
| IIFAA_STATUS_NOT_ENROLLED | 4 | 终端没有录入指纹/人脸 (此时可以引导用户去录入指纹/人脸再做操作)|
| IFAA_STATUS_NOT_REGISTERED | 5 | IFAA 尚未注册 (比如认证/注销/指位更新等操作都需要注册后才可以进行)|
| IFAA_STATUS_REGISTERED | 6 | IFAA 已经注册 (这只是一个状态，并不是错误)|
| IFAA_STATUS_PASSCODE_NOT_SET | 7 | 尚未设置屏幕锁密码（IFAA 需要设置屏幕锁后才能进行，否则不安全，此处可引导用户去设置屏幕锁，iOS独有）|
| IFAA_CLIENT_ERROR | 8 | 本地执行异常 (错误发生在app执行过程中)|
| IFAA_SERVER_ERROR | 9 | IFAA 服务器错误 （此错误发生在服务器）|
| IFAA_STATUS_DELETED | 10 | 本地指纹已经注册，但是注册的指纹模组数据已经被删除 |
| IFAA_CLIENT_ERROR_MULTI_FP_NOT_SUPPORT | 11 | 此手机不支持多指位 |
| IFAA_STATUS_RESULT_CANCELED | 12 | 用户取消 |
| IFAA_STATUS_RESULT_TIMEOUT | 13 | 本地指纹认证超时（APP提示用户按压指纹）|
| IFAA_STATUS_RESULT_AUTH_ FAI | 14 | 验证失败，系统指纹不匹配（APP提示用户按压本地录入的指纹）|
| IFAA_STATUS_RESULT_SYSTEM_BLOCK | 15 | 连续多次校验失败，指纹校验被暂时锁定（各个厂商实现不同，一般1分钟之内可以解锁，继续使用指纹功能）|
| IFAA_STATUS_RESULT_FALLBACK | 16 | 点击了 FALLBACK 按钮 |
| IFAA_STATUS_RESULT_TEE_ERROR | 17 | TEE 错误（手机厂商底层实现问题，可提示用户更新手机系统版本）|
| IFAA_STATUS_RESULT_SYSTEM_ERROR | 18 | 手机系统问题，请升级系统版本 |
| IFAA_PERMISSION_DENIED | 19 | 当前设备未获取相机权限（认证类型为人脸用户没有赋予相机权限）|
