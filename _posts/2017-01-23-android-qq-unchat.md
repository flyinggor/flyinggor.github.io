---
layout: post
title: 'Android 第三方应用跳转到QQ进行聊天'
date: '2017-01-23'
header-img: "img/post-bg-android.jpg"
tags:
     - android
author: 'GeniusVoler'
---
#跳转QQ聊天代码：
	 
//获取包信息


`public static booleanisQQClientAvailable(Context context) {
finalPackageManager packageManager = context.getPackageManager();
	List pinfo = packageManager.getInstalledPackages(0);
		if(pinfo !=null) {
			for(inti =0;i < pinfo.size();i++) {
			String pn = pinfo.get(i).packageName;
			if(pn.equals("com.tencent.mobileqq")) {
					return true;
			}
		}
	}

	return false;
}`

//跳转QQ

	String url ="mqqwpa://im/chat?chat_type=wpa&uin=你的QQ号";
	if(isQQClientAvailable(getContext())) {
		startActivity(newIntent(Intent.ACTION_VIEW,Uri.parse(url)));
	}else{
		ShortToast.getToast(getContext(),"您的QQ版本过低或您当前未安装QQ,请安装最新版QQ后再试").show();
	}

但跳转的QQ对话框之后，发送消息会提示发送失败，这是因为接收的QQ没有QQ推广功能。具体开通方法如下：1.打开QQ推广网址http://shang.qq.com并用QQ登录2.点击顶部导航栏：推广工具3.在弹出菜单中点击'立即免费开通' 即可。

需要注意的是，开通QQ推广后默认开通的是web端的QQ对话功能，移动端WPA是不开启的，需要手动开启，如下图：

![移动WPA开启截图](http://upload-images.jianshu.io/upload_images/2820810-1116e5975cb0db0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样开启后，移动端的对话就可以了，如需要更深层次的功能，只能去申请企业QQ或者付费了。



> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
