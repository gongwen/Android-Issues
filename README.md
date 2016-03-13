记录Android 开发中遇到的问题
===
##### 1. 使用android.support.design.widget.TabLayout时，crash掉？
        Caused by: java.lang.IllegalStateException: You need to use a Theme.AppCompat theme (or descendant) with this activity.
        Caused by: java.lang.UnsupportedOperationException: Can't convert to color: type=0x2
        解决办法：use a Theme.AppCompat theme
