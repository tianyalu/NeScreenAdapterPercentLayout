### NeScreenAdapterPercentLayout 手写百分比布局适配（类谷歌）
#### 类似谷歌的百分比布局适配，手写自定义View  
#### PercentLayout代码如下所示：
  ```android
    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        //获取父容器的尺寸
        int widthSize = MeasureSpec.getSize(widthMeasureSpec);
        int heightSize = MeasureSpec.getSize(heightMeasureSpec);
        int count = getChildCount();
        for (int i = 0; i < count; i++) {
            View child = getChildAt(i);
            ViewGroup.LayoutParams params = child.getLayoutParams();
            //如果说是百分比布局属性
            if (checkLayoutParams(params)) {
                LayoutParams lp = (LayoutParams) params;
                float widthPercent = lp.widthPercent;
                float heightPercent = lp.heightPercent;
                float marginLeftPercent = lp.marginLeftPercent;
                float marginRightPercent = lp.marginRightPercent;
                float marginTopPercent = lp.marginTopPercent;
                float marginBottomPercent = lp.marginBottomPercent;
    
                if(widthPercent > 0) {
                    params.width = (int) (widthSize * widthPercent);
                }
                if(heightPercent > 0) {
                    params.height = (int) (heightSize * heightPercent);
                }
                if(marginLeftPercent > 0) {
                    ((LayoutParams) params).leftMargin = (int) (widthSize * marginLeftPercent);
                }
                if(marginRightPercent > 0) {
                    ((LayoutParams) params).rightMargin = (int) (widthSize * marginRightPercent);
                }
                if(marginTopPercent > 0) {
                    ((LayoutParams) params).topMargin = (int) (heightSize * marginTopPercent);
                }
                if(marginBottomPercent > 0) {
                    ((LayoutParams) params).bottomMargin = (int) (heightSize * marginBottomPercent);
                }
            }
        }
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
    }
    
    @Override
    protected boolean checkLayoutParams(ViewGroup.LayoutParams p) {
        return p instanceof LayoutParams;
    }
    
    public LayoutParams generateLayoutParams(AttributeSet attrs) {
        return new LayoutParams(getContext(), attrs);
    }
    
    public static class LayoutParams extends RelativeLayout.LayoutParams {
        private float widthPercent;
        private float heightPercent;
        private float marginLeftPercent;
        private float marginRightPercent;
        private float marginTopPercent;
        private float marginBottomPercent;
    
        public LayoutParams(Context c, AttributeSet attrs) {
            super(c, attrs);
            //解析自定义控件
            TypedArray a = c.obtainStyledAttributes(attrs, R.styleable.PercentLayout);
            widthPercent = a.getFloat(R.styleable.PercentLayout_widthPercent, 0);
            heightPercent = a.getFloat(R.styleable.PercentLayout_heightPercent, 0);
            marginLeftPercent = a.getFloat(R.styleable.PercentLayout_marginLeftPercent, 0);
            marginRightPercent = a.getFloat(R.styleable.PercentLayout_marginRightPercent, 0);
            marginRightPercent = a.getFloat(R.styleable.PercentLayout_marginRightPercent, 0);
            marginBottomPercent = a.getFloat(R.styleable.PercentLayout_marginBottomPercent, 0);
            a.recycle();
        }
    }
```

#### 示例如下图所示：  
![image](https://github.com/tianyalu/NeScreenAdapterPercentLayout/blob/master/show/show.png)
