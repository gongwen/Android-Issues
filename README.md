记录Android 开发中遇到的问题
===
##### 1. 使用android.support.design.widget.TabLayout时，crash掉？
        Caused by: java.lang.IllegalStateException: You need to use a Theme.AppCompat theme (or descendant) with this activity.
        Caused by: java.lang.UnsupportedOperationException: Can't convert to color: type=0x2
        解决办法：use a Theme.AppCompat theme
##### 2. Scrollview嵌套ViewPager时，ViewPager不显示或者不完全显示？
        重写ViewPager的onMeasure方法即可.如下：
        int mHeight = 0;
        @Override
        protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
                for (int i = 0; i < getChildCount(); i++) {
                        View child = getChildAt(i);
                        child.measure(widthMeasureSpec, MeasureSpec.makeMeasureSpec(0, MeasureSpec.UNSPECIFIED));
                        int h = child.getMeasuredHeight();
                        if (h > mHeight){
                                mHeight = h;
                        }
                }
                heightMeasureSpec = MeasureSpec.makeMeasureSpec(mHeight, MeasureSpec.EXACTLY);
                super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        }
##### 3.OuterFragment嵌套InnerFragment时，ViewPager 加载 InnerFragment 出现空白页的情况？
        The definition of getChildFragmentManager() is:
                Return a private FragmentManager for placing and managing Fragments inside of this Fragment.
        Meanwhile the definition of getFragmentManager() (or in this case getSupportFragmentManager()) is:
                Return the FragmentManager for interacting with fragments associated with this fragment's activity.

        Basically, the difference is that Fragment's now have their own internal FragmentManager that can handle Fragments. The child         FragmentManager is the one that handles Fragments contained within only the Fragment that it was added to. The other                  FragmentManager is contained within the entire Activity.

        In this case, what I'm guessing is you've added the Fragments to the Activity's FragmentManager. You get the child                    FragmentManager which doesn't contain what you are looking for. Thus you get the exception because it can't find the Fragment         with the given ID because it's in a different FragmentManager.


