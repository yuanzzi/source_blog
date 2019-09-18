---
layout: post
date: 2019-02-26 14:31:31
cover: false
title: Spring 项目实现简单的多线程定时同步任务
categories:
	- Java
tags:
	- Spring
---

Spring 项目实现简单的多线程定时同步任务

<!-- more -->
 

```JAVA
	//1 在contextListener 直接定义调用3个线程
	public class ContextListener implements ServletContextListener{
	
	@Override
	public void contextInitialized(ServleteContextEvent sce ){
		Thread t1 = new Thread(new Runnable(){
			@Override
			public void run(){
				try{
					while(true){
						com.test.ApplySynManager.getInstance().synMain();
						Thread.sleep(60 * 1000);
					}
				}catch(){
					e.printStackTrace();
				}
			}
		});

		Thread t2 = new Thread(new Runnable(){
			...
		});

		Thread t3 = new Thread(new Runnable(){
			@Override
			public void run(){
				...
		});

		t1.start();
		t2.start();
		t3.start();
	}

	//2、单例模式管理线程
	public class ApplySynManager{
		private ApplySynManager(){}
		private ApplySynManager examApp = null;
		//单例模式，保持这个对象  
	    public static ApplySynManager getInstance(){  
	        if (examApp == null) {  
	            //当flag == true时，为了解决，timer.cancel()后，重新创建一个timer  
	        	examApp = new ExamApplySynManager();    
	        }
	        return examApp;
	    }
		
		public void synMain(){
			if(DefCommon.syncExamThread == DefCommon.THREAD_RUNING){
				FunCommon.printLog("线程运行中synExamMain");
				return FunCommon.getReturnJson(DefCommon.E_Fail,"syncExamThread,线程运行中");
			}
			DefCommon.syncExamThread = DefCommon.THREAD_RUNING;
			
			//业务处理...
			
			//线程标记为结束
			DefCommon.syncExamThread = DefCommon.THREAD_STOP;
			return;
		}
		
		public void synReport(){
			...
			//对应t2
		}
		
		public void synDcm(){
			...
			//对应t3
		}
	
	}
```