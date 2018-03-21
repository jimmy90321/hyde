---
layout     : post
title      : "[筆記]如何使Android APP能夠使用網路功能"
date       : 2018-03-10 00:30:09
author     : "Jimmy"
---
當你開發的Android APP需要使用上網功能，第一個遇到的問題一定是如何開啟網路權限，以下是解決辦法：
1.	打開AndroidManifest.xml (以Android Studio為例)  
![Alt text](/public/image/AndroidManifest.png)

2.	加入以下程式碼  
	&lt;uses-permission android:name="android.permission.INTERNET">&lt;/uses-permission>  	
恭喜你!現在你的APP可以連上網路了!