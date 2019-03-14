

<div style="text-align:center;font-size:200%;font-weight:bold;">ME政通SDK对接文档</div>

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
	  <td style="text-align:center;">2018/04/13</td>
	  <td style="text-align:center;">1.0.0</td>
	  <td style="text-align:center;">初稿</td>
	  <td style="text-align:center;">黄子烨</td>
	</tr>
	<tr  style="height:35px">
	  <td style="text-align:center;">2018/10/15</td>
	  <td style="text-align:center;">1.0.1</td>
	  <td style="text-align:center;">SDK接口更新</td>
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
</table>

<br />
<br />





<span style="font-size:200%;">1. 引言</span>


<span style="font-size:150%;">1.1 概述</span>


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文档主要介绍了ME政通SDK的集成要求、接口调用方式以及在对接过程中常见的问题等；本文适用于包括业务方集成ME政通SDK的Android客户端开发人员以及项目对接中的其他相关人员等。



<span style="font-size:150%;">1.2 开发工具及编程语言</span>

开发工具：`Android Studio 3.+`

编程语言：`Java`

<span style="font-size:150%;">1.3 运行环境</span>

ME政通SDK仅支持真机运行，不支持模拟器。<br />
ME政通SDK支持Android版本`4.0.3`及以上系统。

<span style="font-size:150%;">1.4 名词解释</span>



<table style="width:100%; border-collapse: collapse;">
	<tr style="height:35px">
	  <th>名词</th>
	  <th>释义</th>
	</tr>
	<tr style="height:35px;">
	    <td></td>
	    <td></td>
	</tr>
	<tr  style="height:35px">
	  <td></td>
	  <td></td>
	</tr>
	<tr  style="height:35px">
	  <td></td>
	  <td></td>
	</tr>
	<tr  style="height:35px">
	  <td></td>
	  <td></td>
	</tr>
</table>





<span style="font-size:200%;">2. SDK提供方式</span>

ME政通SDK以`aar`包的形式提供。




<span style="font-size:200%;">3. 集成步骤</span>

1. 在您的工程中，创建`libs`目录（若已有libs则不需要新建）。
2. 将`aar`包拷贝到`libs`下。
3. 在app下的`build.gradle`中的添加如下配置。
4. 把应用包名的`HASH`值发送给移动密码设备服务平台(`ZJCA`)，该平台会分配一个与之对应的`appId`。


```
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
        flatDir {
            dirs 'libs'
        }
    }
}

dependencies {
    ...
    implementation(name: 'aar包名称', ext: 'aar')
    ...
}
```
5. 权限配置
 
在`AndroidManifest.xml`中配置如下权限

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```



<span style="font-size:200%;">4. 接口说明</span>

<br />

<span style="font-size:150%;">4.1 获取传PIN不缓存密码设备实例</span>


<table>
	<tr>
		<td><b>功能描述</b></td>
		<td>获取传PIN不缓存密码设备实例</td>
	</tr>
	<tr>
		<td><b>函数原型</b></td>
		<td>public static MKeyWithPin getMKeyInstance();</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td>ZJCAUtil.getMKeyInstance();</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td>MKeyWithPin</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td></td>
	</tr>
</table>


<br />


<span style="font-size:150%;">4.2 获取证书操作类实例</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取证书操作类实例</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static CertOperWithPin getCertOperInstance(Context context, String userScene);</td>
	</tr>
		<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getCertOperInstance(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">CertOperWithPin</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>


<br />

<span style="font-size:150%;">4.3 获取签名类实例</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取签名类实例</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static SignatureWithPin getSignatureInstance(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getSignatureInstance(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">SignatureWithPin </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>


<br />

<span style="font-size:150%;">4.4 获取对称加解密类实例</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取对称加解密类实例</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static Symmetric getSymmetricInstance(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getSymmetricInstance(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">Symmetric </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>



<br />

<span style="font-size:150%;">4.5 获取非对称加解密类实例</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取非对称加解密类实例</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static AsymmetricWithPin getAsymmetricInstance(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getAsymmetricInstance(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">AsymmetricWithPin </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>



<br />


<span style="font-size:150%;">4.6 初始化移动密码设备</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">初始化移动密码设备</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static void init(Context context, String appId, String userId, InitializeCallBack callBack);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>appId</td>
		<td>String</td>
		<td>业务编号，由移动密码设备服务平台分配的唯一标识</td>
	</tr>
	<tr>
		<td>userId</td>
		<td>String</td>
		<td>用户唯一标识</td>
	</tr>
	<tr>
		<td>callBack</td>
		<td>InitializeCallBack </td>
		<td>回调函数，在回调函数中通知结果</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.init(context, appId, userId, callBack);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">AsymmetricWithPin </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>


<br />


<span style="font-size:150%;">4.7 对称加密初始化</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称加密初始化</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static ResultVo symEncryptInit(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptInit(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">ResultVo </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>




<br />


<span style="font-size:150%;">4.8 对称解密初始化</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称解密初始化</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static ResultVo symDecryptInit(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptInit(context, userScene);</td>
	</tr>
	<tr>
		<td><b>返回值类型</b></td>
		<td colspan="3">ResultVo </td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>





<br />


<span style="font-size:150%;">4.9 申请个人证书</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">申请个人证书</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static void applyCert(final Context context, String appId, String userId, final String userScene, final User user, final String pin, final int month, final ApplyCertCallBack callBack);</td>
	</tr>
	<tr>
		<td rowspan="9" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>appId</td>
		<td>String </td>
		<td>业务编号，由移动密码设备服务平台分配的唯一标识</td>
	</tr>
	<tr>
		<td>userId</td>
		<td>String</td>
		<td>用户唯一标识</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>user</td>
		<td>User</td>
		<td>申请证书的个人信息，详见<b>用户信息User</b></td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String</td>
		<td>用户访问PIN</td>
	</tr>
	<tr>
		<td>month</td>
		<td>int</td>
		<td>证书有效期，单位为月</td>
	</tr>
	<tr>
		<td>callBack</td>
		<td>ApplyCertCallBack</td>
		<td>回调函数，在回调函数中通知结果</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.applyCert(context, appId, userId, userScene, user, pin, month, callBack);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">无</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>



<br />


<span style="font-size:150%;">4.10 重发个人证书</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">重发个人证书</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static void retryCert(final Context context, String appId, String userId, final String userScene, final User user, final String pin, final int month, final ApplyCertCallBack callBack);</td>
	</tr>
	<tr>
		<td rowspan="9" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context </td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>appId</td>
		<td>String </td>
		<td>业务编号，由移动密码设备服务平台分配的唯一标识</td>
	</tr>
	<tr>
		<td>userId</td>
		<td>String</td>
		<td>用户唯一标识</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>user</td>
		<td>User</td>
		<td>申请证书的个人信息，详见<b>用户信息User</b></td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String</td>
		<td>用户访问PIN</td>
	</tr>
	<tr>
		<td>month</td>
		<td>int</td>
		<td>证书有效期，单位为月</td>
	</tr>
	<tr>
		<td>callBack</td>
		<td>ApplyCertCallBack</td>
		<td>回调函数，在回调函数中通知结果</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.retryCert(context, appId, userId, userScene, user, pin, month, callBack);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">无</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>





<br />


<span style="font-size:150%;">4.11 获取证书基本信息</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取证书基本信息</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String getCertInfo(Context context, String userScene, int type);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>type</td>
		<td>int</td>
		<td>用户信息项类型，详见<b>用户信息项类型</b></td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getCertInfo(context, userScene, type);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>

<br />








<br />


<span style="font-size:150%;">4.12 获取用户在本设备上所有证书列表</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取用户在本设备上所有证书列表</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static UserCert getUserCertList(Context context);</td>
	</tr>
	<tr>
		<td rowspan="2" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getUserCertList(context);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">UserCert</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>






<br />


<span style="font-size:150%;">4.13 获取本设备上所有用户证书列表</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">获取本设备上所有用户证书列表</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static List&lt;UserCert&gt; getAllUserCertList(Context context);</td>
	</tr>
	<tr>
		<td rowspan="2" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.getAllUserCertList(context);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">List&lt;UserCert&gt;</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>




<br />


<span style="font-size:150%;">4.14 数据签名</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">数据签名</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static SignResultVo signData(Context context, String userScene, String inputData, String pin);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>String </td>
		<td>待签名数据</td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String </td>
		<td>用户PIN</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.signData(context, userScene, hash, pin);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">SignResultVo</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>








<br />


<span style="font-size:150%;">4.15 数据Hash签名</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">数据Hash签名</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static SignResultVo signDataByHash(Context context, String userScene, String hash, String pin);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>hash</td>
		<td>String </td>
		<td>待签名数据（使用SM3算法做hash）</td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String </td>
		<td>用户PIN</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.signDataByHash(context, userScene, hash, pin);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">SignResultVo</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>







<br />


<span style="font-size:150%;">4.16 数据签名验证</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">数据签名验证</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static boolean verifySignedData(Context context, String userScene, String signature, String inputData, String cert);</td>
	</tr>
	<tr>
		<td rowspan="6" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>signature</td>
		<td>String </td>
		<td>签名值 base64编码</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>String </td>
		<td>原文</td>
	</tr>
		<tr>
		<td>cert</td>
		<td>String </td>
		<td>证书   base64编码</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.verifySignedData(context, userScene, signature, inputData, cert);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">boolean</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>





<br />


<span style="font-size:150%;">4.17 导入会话密钥</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">导入会话密钥</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static void importSessionKey(Context context, String userScene, String sessionKey, ResultCallBack resultCallBack);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>sessionKey</td>
		<td>String </td>
		<td>会话密钥</td>
	</tr>
	<tr>
		<td>resultCallBack</td>
		<td>ResultCallBack </td>
		<td>回调函数，在回调函数中通知结果</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.importSessionKey(context, userScene, sessionKey, resultCallBack);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">无</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>







<br />


<span style="font-size:150%;">4.18 对称加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String symEncryptData(Context context, String userScene, String inputData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>String </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptData(context, userScene, inputData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>







<br />


<span style="font-size:150%;">4.19 对称加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symEncryptData(Context context, String userScene, byte[] inputData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>byte[] </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptData(context, userScene, inputData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>








<br />


<span style="font-size:150%;">4.20 对称解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String symDecryptData(Context context, String userScene, String decryptData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>decryptData</td>
		<td>String </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptData(context, userScene, decryptData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>





<br />


<span style="font-size:150%;">4.21 对称解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symDecryptData(Context context, String userScene, byte[] decryptData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>decryptData</td>
		<td>byte[] </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptData(context, userScene, decryptData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>









<br />


<span style="font-size:150%;">4.22 非对称加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">非对称加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String asyPubKeyEncryptData(Context context, String userScene, String cert, String inputData);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>cert</td>
		<td>String </td>
		<td>加密使用的证书串base64编码</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>String </td>
		<td>待加密数据信息</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.asyPubKeyEncryptData(context, userScene, cert, inputData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>






<br />


<span style="font-size:150%;">4.23 非对称加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">非对称加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] asyPubKeyEncryptData(Context context, String userScene, String cert, byte[] inputData);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>cert</td>
		<td>String </td>
		<td>加密使用的证书串base64编码</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>byte[] </td>
		<td>待加密数据信息</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.asyPubKeyEncryptData(context, userScene, cert, inputData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>









<br />


<span style="font-size:150%;">4.24 非对称解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">非对称解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String asyPriKeyDecryptData(Context context, String userScene, String encData, String pin);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>encData</td>
		<td>String </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String </td>
		<td>用户访问PIN</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.asyPriKeyDecryptData(context, userScene, encData, pin);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>







<br />


<span style="font-size:150%;">4.25 非对称解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">非对称解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] asyPriKeyDecryptData(Context context, String userScene, byte[] encData, String pin);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>encData</td>
		<td>byte[] </td>
		<td>待解密数据 base64编码</td>
	</tr>
	<tr>
		<td>pin</td>
		<td>String </td>
		<td>用户访问PIN</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.asyPriKeyDecryptData(context, userScene, encData, pin);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>












<br />


<span style="font-size:150%;">4.26 导出用户的签名证书</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">导出用户的签名证书</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String exportSignCert(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.exportSignCert(context, userScene);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>







<br />


<span style="font-size:150%;">4.27 导出用户的加密证书</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">导出用户的加密证书</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static String exportEncCert(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.exportEncCert(context, userScene);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">String</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>











<br />


<span style="font-size:150%;">4.28 对称分组加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symEncryptUpdate(Context context, String userScene, byte[] encryptData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>encryptData</td>
		<td>byte[] </td>
		<td>待加密数据</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptUpdate(context, userScene, encryptData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>








<br />


<span style="font-size:150%;">4.29 对称分组加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symEncryptFinal(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptFinal(context, userScene);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3">在对称加密完数据后调用</td>
	</tr>
</table>












<br />


<span style="font-size:150%;">4.30 对称分组解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symDecryptUpdate(Context context, String userScene, byte[] inputData);</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>inputData</td>
		<td>byte[] </td>
		<td>待解密数据</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptUpdate(context, userScene, inputData);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>












<br />


<span style="font-size:150%;">4.31 对称分组解密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组解密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symDecryptFinal(Context context, String userScene);</td>
	</tr>
	<tr>
		<td rowspan="3" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptFinal(context, userScene);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3">在对称解密完数据后调用</td>
	</tr>
</table>










<br />


<span style="font-size:150%;">4.32 对称分组加密数据</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组加密数据</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static byte[] symEncryptDataByGroup(Context context, String userScene, byte[] totalEncryptData, int eachReadLength);</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>totalEncryptData</td>
		<td>byte[] </td>
		<td>要加密的总数据</td>
	</tr>
	<tr>
		<td>eachReadLength</td>
		<td>int </td>
		<td>每次加密的长度</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symEncryptDataByGroup(context, userScene, totalEncryptData, eachReadLength);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">byte[]</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>





<br />


<span style="font-size:150%;">4.33 对称分组解密</span>


<table>
	<tr>
		<td width="110px"><b>功能描述</b></td>
		<td colspan="3">对称分组解密</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">public static void symDecryptDataByGroup(Context context, String userScene, byte[] totalDecryptData, int eachReadLength, Callback callback);</td>
	</tr>
	<tr>
		<td rowspan="6" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>userScene</td>
		<td>String </td>
		<td>证书使用场景</td>
	</tr>
	<tr>
		<td>totalDecryptData</td>
		<td>byte[] </td>
		<td>要解密的总数据</td>
	</tr>
	<tr>
		<td>eachReadLength</td>
		<td>int </td>
		<td>每次解密的长度</td>
	</tr>
	<tr>
		<td>callback</td>
		<td>Callback </td>
		<td>回调函数</td>
	</tr>
	<tr>
		<td><b>函数调用方式</b></td>
		<td colspan="3">ZJCAUtil.symDecryptDataByGroup(context, userScene, totalDecryptData, eachReadLength, callback);</td>
	</tr>
	<tr>
	    <td><b>返回值类型</b></td>
	    <td colspan="3">无</td>
	</tr>
	<tr>
	    <td><b>备注</b></td>
	    <td colspan="3"></td>
	</tr>
</table>























<br />





<span style="font-size:150%;">4.34 SDK内唤起ME政通APP</span>



<table>
	<tr>
		<td  width="110px" style="vertical-align:middle;"><b>功能描述</b></td>
		<td colspan="3">第三方业务客户端通过调用该接口，可以唤起ME政通执行数据签名、数据解密等操作。</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">ZJCAUtil.skipHandleDataActivity(Context context, String appname, int handleType, int usageType, String data);</td>
	</tr>
	<tr>
		<td rowspan="6" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>appname</td>
		<td>String</td>
		<td>第三方应用名称</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;">handleType</td>
		<td style="vertical-align:middle;text-align:center;">int</td>
		<td>
			第三方app处理数据的操作类型<br />
			1 登录<br />
			2 签名<br />
			3 解密<br />
		</td>
	</tr>
	<tr>
		<td>usageType</td>
		<td style="vertical-align:middle;text-align:center;">int</td>
		<td>
			SDK授权类型
			1 签名
			2 解密
		</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;">data</td>
		<td style="vertical-align:middle;">String</td>
		<td>
			如果handleType为1，则data为任意的非空字符串；<br />
			如果handleType为2，则data为非空字符串的MD5值；<br />
			如果handleType为3，则data为File的MD5值；
		</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>返回值类型</b></td>	
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td colspan="3"><b>参数说明</b></td>
    </tr>
    <tr>
		<td style="vertical-align:middle;">status</td>
		<td style="vertical-align:middle;">String</td>
		<td colspan="3">
	        "success"：成功 <br/>
	        “error"：失败
        </td>
    </tr>
    <tr>
		<td>message</td>
		<td>String</td>
		<td colspan="2">
	        提示信息
        </td>
    </tr>
    <tr>
		<td style="vertical-align:middle;">data</td>
		<td style="vertical-align:middle;">String</td>
		<td colspan="2">
	        当status为”success”时，如果handleType为1时，返回数据详见<b>登录返回示例代码</b>；<br/>
如果handleType为2时，返回数据详见<b>签名返回示例代码</b>；<br/>
如果handleType为3时，返回数据详见<b>解密返回示例代码</b>；
        </td>
    </tr>
    <tr>
        <td><b>备注</b></td>
        <td colspan="3"></td>
    </tr>
</table>



<br />








<span style="font-size:150%;">4.35 唤起ME政通APP</span>



<table>
	<tr>
		<td  width="110px" style="vertical-align:middle;"><b>功能描述</b></td>
		<td colspan="3">第三方业务客户端通过调用该接口，可以唤起ME政通执行数据签名、数据解密等操作。</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;"><b>函数原型</b></td>
		<td colspan="3">
<pre>
Uri uri = Uri.parse("urlscheme://handle_activity");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
intent.putExtra("appname", appname);
intent.putExtra ("handleType", handleType);
intent.putExtra("data", data);
startActivityForResult(intent, 10);
</pre>
		</td>
	</tr>
	<tr>
		<td rowspan="5" style="vertical-align:middle;"><b>参数</b></td>
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td><b>参数说明</b></td>
	</tr>
	<tr>
		<td>context</td>
		<td>Context</td>
		<td>上下文对象</td>
	</tr>
	<tr>
		<td>appname</td>
		<td>String</td>
		<td>第三方应用名称</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;">handleType</td>
		<td style="vertical-align:middle;text-align:center;">int</td>
		<td>
			第三方app处理数据的操作类型<br />
			1 登录<br />
			2 签名<br />
			3 解密<br />
		</td>
	</tr>
	<tr>
		<td style="vertical-align:middle;">data</td>
		<td style="vertical-align:middle;">String</td>
		<td>
			如果handleType为1，则data为任意的非空字符串；<br />
			如果handleType为2，则data为非空字符串的MD5值；<br />
			如果handleType为3，则data为File的MD5值；
		</td>
	</tr>
	<tr>
		<td rowspan="4" style="vertical-align:middle;"><b>返回值类型</b></td>	
		<td><b>参数名</b></td>
		<td><b>参数类型</b></td>
		<td colspan="3"><b>参数说明</b></td>
    </tr>
    <tr>
		<td style="vertical-align:middle;">status</td>
		<td style="vertical-align:middle;">String</td>
		<td colspan="3">
	        "success"：成功 <br/>
	        “error"：失败
        </td>
    </tr>
    <tr>
		<td>message</td>
		<td>String</td>
		<td colspan="2">
	        提示信息
        </td>
    </tr>
    <tr>
		<td style="vertical-align:middle;">data</td>
		<td style="vertical-align:middle;">String</td>
		<td colspan="2">
	        当status为”success”时，如果handleType为1时，返回数据详见<b>登录返回示例代码</b>；<br/>
如果handleType为2时，返回数据详见<b>签名返回示例代码</b>；<br/>
如果handleType为3时，返回数据详见<b>解密返回示例代码</b>；
        </td>
    </tr>
    <tr>
        <td><b>备注</b></td>
        <td colspan="3"></td>
    </tr>
</table>





<br />


<span style="font-size:150%;">5. Android 平台数据类型定义</span>



**5.1 用户信息User**




| 属性 | 属性类型 | 属性名称 | 备注 |
| --- | --- | --- | --- |
| userName | String | 用户姓名 |  | 
| cardType | int | 证件类型 | 1 身份证号  |
| cardNO | String | 证件号码 |  | 
| mobile | String | 手机号码 |	 | 
| address | String | 通讯地址 |	 | 
| zipcode | String | 邮政编码 |	 | 
| email | String | 电子邮件	 | | 
| gender | int | 用户性别	 | 1 男 2 女 |
| province | String | 省份	 | | 
| city | String | 城市	 | | 
| unit | String | 所在机构或部门 | 	 |
| org | String | 所在组织或单位 | 	 |
| country | String | 国家 | 默认中国 CN |


> 必填项：`username`、`cardType`、`cardNO`。



<br />

**5.2 用户信息项类型**

| type | 说明 |
| --- | --- |
| 1	| 证书版本 |
| 2	| 证书的用户通用名CommonName |
| 3	| 证书序列号 |
| 4	| 证书发放者国家名 |
| 5	| 证书发放者组织名 |
| 6	| 证书发放者部门名 |
| 7	| 证书发放者省州名 |
| 8	| 证书发放者通用名 |
| 9	| 证书发放者城市名 |
| 10	| 证书发放者EMAIL地址 |
| 11	| 证书有效期起始 |
| 12	| 证书有效期截止 |
| 13	| 用户国家名 |
| 14	| 用户组织名 | |
| 15	| 用户部门名 |
| 16	| 用户省州名 |
| 17	| 用户通用名 |
| 18	| 用户城市名 |
| 19    | 用户EMAIL地址 |


<br />

**5.3 唤起ME政通APP 示例代码**



<br />

```java
package com.zjca.test;

import android.content.Intent;
import android.os.Bundle;
import android.support.annotation.Nullable;
import android.support.v7.app.AppCompatActivity;
import android.text.TextUtils;
import android.util.Log;
import android.view.View;
import android.widget.Button;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.zjca.test.util.ToastUtil;
import com.zjca.mztsdk.util.ZJCAUtil;


public class LoginActivity extends AppCompatActivity implements View.OnClickListener {

    private Button btnLogin;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        btnLogin = (Button) findViewById(R.id.btn_login);
        btnLogin.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_login:
                try {
                    ZJCAUtil.skipHandleDataActivity(LoginActivity.this, "app应用名称", 1, 1, "zjca");
                } catch (Exception e) {
                    e.printStackTrace();
                }
                break;
        }
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        switch (requestCode) {
            case ZJCAUtil.SKIP_HANDLE_DATA_REQUEST_CODE:
                if (resultCode == RESULT_OK) {
                    final String result = data.getStringExtra("data");
                    JSONObject object = JSON.parseObject(result);
                    if ("success".equals(object.getString("status"))) {
                        String resultData = object.getString("data");
                        if (!TextUtils.isEmpty(resultData)) {
                            JSONObject obj = JSON.parseObject(resultData);
                            if ("success".equals(obj.getString("status"))) {
                                JSONObject o = JSON.parseObject(obj.getString("data"));
                                //获取手机号
                                String cellphone = o.getString("cellphone");
                                //获取用户token
                                String token = o.getString("token");
                                //获取用户id
                                String userId = o.getString("userId");
                                //获取签名证书
                                String signCert = o.getString("signCert");
                                Log.i("tag", signCert);
                            } else {
                                ToastUtil.showShort(LoginActivity.this, obj.getString("message"));
                            }
                        } else {
                            ToastUtil.showShort(LoginActivity.this, object.getString("message"));
                        }
                    }
                }
                break;
        }
    }
}
```

<br />


**5.4 登录返回示例代码**


<br />

```java
package com.zjca.test;

import android.content.Intent;
import android.os.Bundle;
import android.support.annotation.Nullable;
import android.support.v7.app.AppCompatActivity;
import android.text.TextUtils;
import android.util.Log;
import android.view.View;
import android.widget.Button;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.zjca.test.util.ToastUtil;
import com.zjca.mztsdk.util.ZJCAUtil;


public class LoginActivity extends AppCompatActivity implements View.OnClickListener {

    private Button btnLogin;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        btnLogin = (Button) findViewById(R.id.btn_login);
        btnLogin.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_login:
                try {
                    ZJCAUtil.skipHandleDataActivity(LoginActivity.this, "app应用名称", 1, 1, "zjca");
                } catch (Exception e) {
                    e.printStackTrace();
                }
            break;
        }
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        switch (requestCode) {
            case ZJCAUtil.SKIP_HANDLE_DATA_REQUEST_CODE:
                if (resultCode == RESULT_OK) {
                    final String result = data.getStringExtra("data");
                    JSONObject object = JSON.parseObject(result);
                    if ("success".equals(object.getString("status"))) {
                        String resultData = object.getString("data");
                        if (!TextUtils.isEmpty(resultData)) {
                            JSONObject obj = JSON.parseObject(resultData);
                            if ("success".equals(obj.getString("status"))) {
                                JSONObject o = JSON.parseObject(obj.getString("data"));
                                //获取手机号
                                String cellphone = o.getString("cellphone");
                                //获取用户token
                                String token = o.getString("token");
                                //获取用户id
                                String userId = o.getString("userId");
                                //获取签名证书
                                String signCert = o.getString("signCert");
                                Log.i("tag", signCert);
                            } else {
                                ToastUtil.showShort(LoginActivity.this, obj.getString("message"));
                            }
                        } else {
                            ToastUtil.showShort(LoginActivity.this, object.getString("message"));
                        }
                    }
                }
                break;
        }
    }
}
```

<br />

**5.5 签名返回示例代码**

<br />

```java
package com.zjca.test;

import android.content.Intent;
import android.os.Bundle;
import android.support.annotation.Nullable;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.zjca.test.util.ToastUtil;
import com.zjca.mztsdk.util.ZJCAUtil;

import java.io.File;


public class SignActivity extends AppCompatActivity implements View.OnClickListener {

    private Button btnSign;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sign);
        btnSign = (Button) findViewById(R.id.btn_sign);
        btnSign.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_sign:
                try {
                    ZJCAUtil.skipHandleDataActivity(SignActivity.this, "app应用名称", 2, 1, MD5Util.getFileMD5(new File(path)));
                } catch (Exception e) {
                    e.printStackTrace();
                }
                break;
        }
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        switch (requestCode) {
            case ZJCAUtil.SKIP_HANDLE_DATA_REQUEST_CODE:
                if (resultCode == RESULT_OK) {
                    final String result = data.getStringExtra("data");
                    JSONObject object = JSON.parseObject(result);
                    if (("success").equals(object.getString("status"))) {
                        // 签名数据
                        String signResult = object.getString("data");
                        ToastUtil.showShort(SignActivity.this, "签名成功");
                    } else {
                        ToastUtil.showShort(SignActivity.this, object.getString("message"));
                    }
                }
                break;
        }
    }
}
```

<br />

**5.6 解密返回示例代码**

<br />

```java
package com.zjca.test;

import android.content.Intent;
import android.os.Bundle;
import android.support.annotation.Nullable;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import com.zjca.test.util.ToastUtil;
import com.zjca.mztsdk.util.ZJCAUtil;

public class DecryptActivity extends Activity implements OnClickListener{

    private Button btnDecrypt;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		btnDecrypt = findViewById(R.id.btn_decrypt);
		btnDecrypt.setOnClickListener(this);
	}
	
	@Override
	public void onClick(View view) {
	    switch (view.getId()) {
	        case R.id.btn_decrypt:
	            ZJCAUtil.skipHandleDataActivity(DecryptActivity.this, “app应用名称”, 3, 2, decryptFilePath);
		break;
		}
	}
	
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	    super.onActivityResult(requestCode, resultCode, data);
	    switch (requestCode) {
		    case ZJCAUtil.SKIP_HANDLE_DATA_REQUEST_CODE:
				if (resultCode == RESULT_OK) {
					final String result = data.getStringExtra("data");
					JSONObject object = JSON.parseObject(result);
					if (("success").equals(object.getString("status"))) {
						ToastUtil.showShort(DecryptActivity.this, "解密成功");
					} else {
						ToastUtil.showShort(DecryptActivity.this, object.getString("message"));
					}
				}
	        break;
		}
	}
}
```




<br />


<span style="font-size:150%;">6. 错误代码表</span>



| 标识 | 预定义值 | 说明 |
| --- | --- | --- |
| SAR_SUCCESS | 	0 | 	成功 | 
| SAR_UNKNOWN_ERR | 	0X0B000001	 | 未知错误 | 
| SAR_NOT_SUPPORT_YET_ERR | 	0X0B000002 | 	不支持的服务 | 
| SAR_FILE_OPER_ERR | 	0X0B000003 | 	文件操作错误 | 
| SAR_ALGO_TYPE_ERR | 	0X0B000004 | 	算法类型错误 | 
| SAR_NOT_INITIALIZE | 	0X0B000005 | 	未初始化 | 
| SAR_MEMORY_ERR | 	0X0B000006 | 	内存错误 | 
| SAR_OPER_TIMEOUT_ERR | 	0X0B000007 | 	用户操作超时 | 
| SAR_IN_DATA_LEN_ERR | 	0X0B000008 | 	输入数据长度错误 | 
| SAR_IN_DATA_ERR | 	0X0B000009 | 	输入数据错误 | 
| SAR_SYM_ENC_FAILED | 	0X0B00000A | 	对称加密失败 | 
| SAR_SYM_DEC_FAILED | 	0X0B00000B | 	对称解密失败 | 
| SAR_ASYM_ENC_FAILED | 	0X0B00000C	 | 非对称加密失败 | 
| SAR_ASYM_DEC_FAILED | 	0X0B00000D	 | 非对称解密失败 | 
| SAR_IMPORT_SESSION_KEY_ FAILED | 	0X0B00000E | 	导入会话密钥失败 | 
| SAR_HASH_NOT_EQUAL | 	0X0B00000F | 	  HASH值不相等 | 
| SAR_KEY_NOT_FOUND | 	0X0B000010 | 	密钥未发现 | 
| SAR_CERT_NOT_FOUND | 	0X0B000011 | 	证书未发现 | 
| SAR_MACLEN_ERR | 	0X0B000012 | 	MAC长度错误 | 
| SAR_BUSINESS_APP_ERR | 	0X0B000013	 | 业务客户端非法 | 
| SAR_BUSINESS_NOT_EXIST | 	0X0B000014	 | 业务不存在 | 
| SAR_BUSINESS_LOCKED  | 	0X0B000015	 | 业务已停用 | 
| SAR_BUSINESS_REVOKED | 	0X0B000016 | 	业务已注销 | 
| SAR_CSR_EXIST | 	0X0B000017 | 	CSR文件重复生成 | 
| SAR_CSR_GEN_FAILED | 	0X0B000018 | 	CSR生成失败 | 
| SAR_CERT_EXIST | 	0X0B000019 | 	证书已存在 | 
| SAR_CERT_NOT_EXIST | 	0X0B00001A | 	证书未申请 | 
| SAR_CERT_APPLY_FAILED	 | 0X0B00001B	 | 证书申请失败 | 
| SAR_CERT_UPDATE_FAILED | 	0X0B00001C | 	证书更新失败 | 
| SAR_CERT_DELAY_FAILED	 | 0X0B00001D	 | 证书续期失败 | 
| SAR_CERT_REAPPLY_FAILED | 	0X0B00001E	 | 证书补办失败 | 
| SAR_CERT_UPDATE_USER_INFO_FAILED | 	0X0B00001F | 	证书更新用户信息失败 | 
| SAR_CERT_UPDATE_ENT_INFO_FAILED | 	0X0B000020	 | 证书更新企业信息失败 | 
| SAR_CERT_SAVE_FAILED | 	0X0B000021 | 	保存证书失败 | 
| SAR_ENC_KEY_IMPORT_FAILED | 	0X0B000022 | 	加密密钥对导入失败 | 
| SAR_ENC_KEY_STRU_NOT_SUPPORT | 	0X0B000023 | 	不支持的加密密钥保护结构体 | 
| SAR_CERT_EXPORT_FAILED | 	0X0B000024	 | 证书导出失败 | 
| SAR_CERT_INFO_GET_FAILED | 	0X0B000025 | 	获取证书基本信息项失败 | 
| SAR_CERT_INFO_TYPE_NOT_SUPPORT | 	0X0B000026 | 	不支持的证书信息项 | 
| SAR_CERT_EXT_INFO_GET_FAILED | 	0X0B000027 | 	获取证书扩展信息项失败 | 
| SAR_CERT_EXPIRED | 	0X0B000028 | 	证书已过期 | 
| SAR_CERT_LOCKED | 	0X0B000029 | 	证书已冻结 | 
| SAR_CERT_REVOKED | 	0X0B00002A | 	证书已吊销 | 
| SAR_CERT_NOT_FOUND | 	0X0B00002B | 	未找到符合补办条件的证书 | 
| SAR_PIN_VERIFY_FAILED	 | 0X0B00002C | 	用户PIN验证失败 | 
| SAR_PIN_LOCKED | 	0X0B00002D | 	用户PIN已锁定 | 
| SAR_MKEY_LOCKED | 	0X0B00002E | 	移动密码设备已停用 | 
| SAR_MKEY_REVOKED | 	0X0B00002F | 	移动密码设备已注销 | 
| SAR_NET_CONNECT_TIMEOUT | 	0X0B000030 | 	网络连接超时 | 
| SAR_SIGNATURE_FAILED	 | 0X0B000031 | 	签名失败 | 
| SAR_SIGNATURE_VERIFY_FAILED | 	0X0B000032	 | 签名验证失败 | 
| SAR_FILE_NOT_FOUND | 	0X0B000033 | 	文件未找到 | 
| SAR_FILE_SAVE_FAILED | 	0X0B000034 | 	文件保存失败 | 
| SAR_SESSION_KEY_LEN_ERR | 	0X0B000035 | 	会话密钥长度错误 | 
| SAR_CERT_CODED_ERR | 	0X0B000036	 | 证书编码错误 | 
| SAR_ENV_FAILED | 	0X0B000037 | 	封装PKCS#7数字信封失败 | 
| SAR_DIS_ENV_FAILED | 	0X0B000038 | 	解析PKCS#7数字信封失败 | 
| SAR_ANAL_PKCS7_SIGNATURE_FAILED | 	0X0B000039 | 	解析PKCS#7签名值失败 | 
| SAR_APPLICATION _STOP	 | 0x0B00003A | 	应用已停用 | 
| SAR_APPLICATION _CANCEL | 	0x0B00003B | 	应用已注销 | 
| SAR_APPLICATION _NOT_EXIST | 	0x0B00003C | 	应用不存在 | 








<br />


<span style="font-size:150%;">7. 常见问题</span>



**7.1 Failed to resolve xxx**

出现如下错误

```
Failed to resolve: :zjca-sdk-test:
Open File
```

原因是在编译时没有找到aar的目录，只要在app下的build.gradle 中添加如下配置，然后重新编译即可。


```
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
        flatDir {
            dirs 'libs'
        }
    }
}
```


**7.2 未知错误**


出现未知错误，可能以下情况：


> 1. 请确保在调用SDK其它接口之前，先调用初始化接口（`init`）。
>
>
> 2. 确保安装的应用程序是签过名的，否则也会出现该错误。
>
> 3. `appId`和应用包名`HASH`值不匹配。
>
> 4. 确保是签过名应用程序的应用包名的`HASH`值。


















