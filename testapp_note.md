# 笔记 #


- 选取app图标，按照mh超高清晰度选择即可，不要选低清晰度的，AKA选96px*96px大小的png格式图片。下载网址：http://www.easyicon.net/	可以按颜色、大小、图片格式免费下载。
- 无法启动welcomeAct,空指针-------1，Eclipse在自动修改包名后，清单文件里的package值仍然需要手动修改。2，onCreate里，setContent方法必须要在findviewbyId方法前调用。
- textview的文本不居中------layout_gravity:center
- LinearLayout的子view不居中----------LL的gravity:center
- 手势监听：代码见下
- onTouchEvent方法里，switch语句还没写东西就报错---------把super方法去掉，return true，自己消费事件。
- activity绑定一个service有 has leaked ServiceConnection com.testapp.MainAct@41e6b5c8 that was originally bound here错误---------在act里的onDestroy方法加上unbindSerivce即可。
- service里的callback接口初始化时空指针------加上if判空即可。因为service生命周期是先onCreate再onstartCommand。onstartcommand里才会和activity绑定，所以第一次callback接口肯定为空。
- 在service和activity传递数据：基本思路还是在activity里加一个handler处理接收到的数据。为了让同一个handler收发数据，那么必须在activity里发数据。但是还要让service接收到数据，就应该让service自定义一个接口。接口的作用就是让两个类都必须实现同一个方法。这个接口在activity里的onServiceConnected方法实现。目的是在里面调用service.setCallBack方法，逼迫activity把数据发送操作放到接口的抽象方法的实现里。至于如何确保activity发送的数据确实给到了特定的service里，就要activity和service绑定，通过onServiceConnected方法的参数中得到自定义binder，自定义binder返回了service自身的引用。
- 为了让textview的文本不突变，不要在xml里设置text属性。
- 自定义viewgroup,子view只显示第一个，后面的都不显示--------必须重写onMeasure和onLayout方法（重写时均不调用super方法）。
	- 1，onMeasure必须用setMeasuredDimension方法，里面的宽高值，从MeasureSpec.getSize里得到，getSize的参数从onMeasure的传入参数里得到。子view的宽高直接传入onMeasure的参数即可
	- 2，onLayout方法，子view的左上右下值不能用view.getWidth之类，要用view.getMeasuredWidth之类。
- textview用了params仍然不居中--------不要用params，直接tv.setGravity(Gravity.CENTER)即可
- textview之间，虽然是包裹内容，但是设置了margin ,却有一部分字被挡住了-----view.onLayout参数错误，top值写成了sizeHeight+params.Topmargin。但其实，onMeasure里已经把margin值算入height里了，所以得到的sizeHeight是包含margin值的。再添加margin值，就从本身view的高度里缩小view的显示高度，挤出来空白空间给这多余的margin值，从而造成margin值遮挡textview的文本。
- margin值设置失效-------
	- 1，在LinearLayout布局里，应该使用LinearLayout.LayoutParams，而不是MarginLayoutParams，因为前者已经继承后者。如果使用的是MarginLayoutParams，则源码认为是无效的。
	- 2，去掉onMeasure和onLayout方法，finish。因为你继承了LinearLayout，在Linearlayout类中的onMeasure和onlayout方法已经实现了你想实现的逻辑。不需要额外重写。**所以，自定义的五大布局，只要不是直接继承viewgroup，都不需要重写这两个方法（除非你想在五大布局的基础上定制自己的布局逻辑
）。如果是直接继承viewgroup，只需要重写onLayout方法。**
- Caused by: java.lang.IllegalStateException: The specified child already has a parent. You must call removeView() on the child's parent first.--------用布局xml通过inflate来的，系统认为是同一个view，放入循环中inflate，然后addview，问题解决。
- 的







----------
# 代码 #
		
		1./*滑动手势监听*/
    	@Override
    	public boolean onTouchEvent(MotionEvent event) {
    		switch (event.getAction()) {
    		case MotionEvent.ACTION_DOWN:
    			lastX = (int) event.getRawX();
    			break;
    
    		case MotionEvent.ACTION_UP:
    			if (Math.abs(lastX-event.getRawX()) <= MIN_DISTANCE) {
    				break;
    			}else {
    				if (lastX < event.getRawX()) {
    					//滑到上一页
    					Toast.makeText(ctx, "上一页", 0).show();
    				}
    				if (lastX > event.getRawX()) {
    					//滑到下一页
    					Toast.makeText(ctx, "下一页", 0).show();
    				}
    			}
    			break;
    		}
    		
    		return true;
    	}

	2./*自定义service的实现*/
	public class CountTimeService extends Service {
	private CallBack callBack;
	private boolean connecting = false;

	@Override
	public void onCreate() {
		connecting = true;
		super.onCreate();
		new Thread(new Runnable() {
			int count = getTime();
			@Override
			public void run() {
				while (connecting) {
					if (callBack != null) {
						// translate data to activity
						callBack.onDataChange(count + "");
					}
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
					count--;
				}

				if (count <= 0) {
					stopSelf();
				}
			}
		}).start();

	}

	public int getTime() {
		return 7300;
	}

	@Override
	public IBinder onBind(Intent intent) {
		return new TimeBinder();
	}

	public class TimeBinder extends Binder {
		public CountTimeService geTimeService() {
			return CountTimeService.this;
		}
	}

	public interface CallBack {
		void onDataChange(String data);
	}

	public void setCallBack(CallBack callBack) {
		this.callBack = callBack;
	}

	@Override
	public void onDestroy() {
		super.onDestroy();
		connecting = false;
		}
	}



