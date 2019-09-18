---
layout: post
date: 2018-11-13
title: Java 实现 HTTP 请求的三种方式
cover: false
categories:
	- 笔记
tags:
	- Java
	- Http
---
  

HttpURLConnection 是 JAVA 最原生的HTTP请求类。HttpClient 是 Apache Jakarta Common 下的子项目，用来提供高效的、最新的、功能丰富的支持 HTTP 协议的客户端编程工具包。
<!-- more -->
#### > 由JAVA网络爬虫延伸开  
### 1. HttpURLConnection
HttpURLConnection 是 JAVA 最原生的HTTP请求类。HttpURLConnection 的 connect() 函数，实际上只是建立了一个服务器的 tcp 连接,并没有实际发送http请求。

无论是用 post 还是 get , http 请求实际上直到 HttpURLConnection 的 getInputStream() 这个函数里面才正式发送出去。  

&emsp;&emsp;在用 Post 方式发送请求时， URL 请求参数的设定顺序是重中之重，对 connection 对象的一切配置(那一堆set函数) 都必须在函数 connect() 执行之前完成。 
OutputStream的写操作， 必须在InputStream 的读操作之前。  


```JAVA

	// 创建远程url连接对象
	URL url = new URL(httpurl);
	// 通过远程url连接对象打开一个连接，强转成httpURLConnection类
	connection = (HttpURLConnection) url.openConnection();
	// 设置连接方式：get
	connection.setRequestMethod("GET");
	// 设置连接主机服务器的超时时间：15000毫秒
	connection.setConnectTimeout(15000);
	// 设置读取远程返回的数据时间：60000毫秒
	connection.setReadTimeout(60000);
	// 发送请求
	connection.connect();
	// 通过connection连接，获取输入流
	if (connection.getResponseCode() == 200) {
	    is = connection.getInputStream();
	    // 封装输入流is，并指定字符集
	    br = new BufferedReader(new InputStreamReader(is, "UTF-8"));
	    // 存放数据
	    StringBuffer sbf = new StringBuffer();
	    String temp = null;
	    while ((temp = br.readLine()) != null) {
	        sbf.append(temp);
	        sbf.append("\r\n");
	    }
	    result = sbf.toString();
	}
	
```

<br>

### 2. HttpClient

HttpClient 是 Apache Jakarta Common 下的子项目，用来提供高效的、最新的、功能丰富的支持 HTTP 协议的客户端编程工具包，并且它支持 HTTP 协议最新的版本和建议。
HttpClient 已经应用在很多的项目中，比如 Apache Jakarta 上很著名的另外两个开源项目 Cactus 和 HTMLUnit 都使用了 HttpClient。

> 以下代码截取于自写爬虫之发送请求类

```Java

	HttpClient httpClient = new HttpClient();
	// 设置 HTTP 连接超时 5s
	httpClient.getHttpConnectionManager().getParams().setConnectionTimeout(5000);
	// 生成 GetMethod 对象并设置参数
	GetMethod getMethod = new GetMethod(url);
	// 设置 get 请求超时 5s
	getMethod.getParams().setParameter(HttpMethodParams.SO_TIMEOUT, 5000);
	// 设置请求重试处理
	getMethod.getParams().setParameter(HttpMethodParams.RETRY_HANDLER, new DefaultHttpMethodRetryHandler(5,true));
	// 执行 HTTP GET 请求
	
	// 4.处理 HTTP 响应内容
	// byte[] responseBody = getMethod.getResponseBody();// 读取为字节 数组
	    
	String contentType = getMethod.getResponseHeader("Content-Type").getValue(); // 得到当前返回类型
	byte[] responseBody = toByteArray( getMethod.getResponseBodyAsStream());// 读取为字节 数组    

```

<br>

### 3. CloseableHttpClient
&emsp;&emsp;CloseableHttpClient 是 HttpClient 的帮助类 ( CloseableHttpClient 继承了 HttpClient 接口 )

> 以下代码截取于自写爬虫之发送请求类

```JAVA

		// 设置连接超时时间
    	RequestConfig defaultRequestConfig = RequestConfig.custom()
    		    .setSocketTimeout(5000)
    		    .setConnectTimeout(5000)
    		    .setConnectionRequestTimeout(5000)
    		    .build();
    	// 生成CloseableHttpClient对象
    	//CloseableHttpClient httpClient = HttpClients.createDefault();
    	CloseableHttpClient httpclient = HttpClients.custom()
    		    .setDefaultRequestConfig(defaultRequestConfig)
    		    .build();
    	CloseableHttpResponse response = null;
    	
    	HttpGet httpGet = new HttpGet(url);
		httpGet.setHeader("User-Agent", "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0");
		
		String contentType =  entity.getContentType().getValue();// 得到当前返回类型
		response = httpclient.execute(httpGet);//获取响应
		HttpEntity entity = response.getEntity();

```

<br/>