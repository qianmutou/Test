# 笔记 #


- 选取app图标，按照mh超高清晰度选择即可，不要选低清晰度的，AKA选96px*96px大小的png格式图片。下载网址：http://www.easyicon.net/	可以按颜色、大小、图片格式免费下载。
- 无法启动welcomeAct,空指针-------1，Eclipse在自动修改包名后，清单文件里的package值仍然需要手动修改。2，onCreate里，setContent方法必须要在findviewbyId方法前调用。
- textview的文本不居中------layout_gravity:center
- LinearLayout的子view不居中----------LL的gravity:center
- 手势监听：

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

- onTouchEvent方法里，switch语句还没写东西就报错---------把super方法去掉，return true，自己消费事件。
- s





----------
# 代码 #