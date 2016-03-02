---
layout: post
title: Android程序如何实现开机自启动
category: Android
tags: Android
keywords: Android，自启动
description: Android程序如何实现开机自启动的方法
---
如何实现想360手机助手那样的开机自启动呢，其实很简单，加个广播接收器就好，但是太流氓了会被用户删的

首先写一个receiver

    import android.content.BroadcastReceiver;  
	import android.content.Context;  
	import android.content.Intent;  
  
	public class AutoBootReceiver extends BroadcastReceiver{  
   	    @Override  
    	public void onReceive(Context context, Intent intent) {  
       	 // TODO Auto-generated method stub  
        Intent myIntent = new Intent(context , MainActivity.class);  
        myIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);  
        context.startActivity(myIntent);  
    	}  
      
	} 

再在manifest里静态注册一下

	<receiver android:name="com.haojiazhang.search.AutoBootReceiver" >  
            <intent-filter>  
                <action android:name="android.intent.action.BOOT_COMPLETED" />  
            </intent-filter>  
     </receiver> 


- 注意，此处应该写在application下，与activity同级别。 当Android系统启动完成时会发送全局广播BOOT_COMPLETED，接收到此广播就会执行我们的代码，启动程序了。
- 注意
-
	myIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);

在activity外启动activity时需要加此句话。