### 问题 
  1.怎么滑动
  
```
public class ScrollView extends FrameLayout {




























    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        if (!mFillViewport) {
            return;
        }
        final int heightMode = MeasureSpec.getMode(heightMeasureSpec);
        if (heightMode == MeasureSpec.UNSPECIFIED) {
            return;
        }
        if (getChildCount() > 0) {
            final View child = getChildAt(0);
            final int height = getMeasuredHeight();
            if (child.getMeasuredHeight() < height) {
                final int widthPadding;
                final int heightPadding;
                final FrameLayout.LayoutParams lp = (LayoutParams) child.getLayoutParams();
                final int targetSdkVersion = getContext().getApplicationInfo().targetSdkVersion;
                if (targetSdkVersion >= VERSION_CODES.M) {
                    widthPadding = mPaddingLeft + mPaddingRight + lp.leftMargin + lp.rightMargin;
                    heightPadding = mPaddingTop + mPaddingBottom + lp.topMargin + lp.bottomMargin;
                } else {
                    widthPadding = mPaddingLeft + mPaddingRight;
                    heightPadding = mPaddingTop + mPaddingBottom;
                }

                final int childWidthMeasureSpec = getChildMeasureSpec(
                        widthMeasureSpec, widthPadding, lp.width);
                final int childHeightMeasureSpec = MeasureSpec.makeMeasureSpec(
                        height - heightPadding, MeasureSpec.EXACTLY);
                child.measure(childWidthMeasureSpec, childHeightMeasureSpec);
            }
        }
    }


   



}

```