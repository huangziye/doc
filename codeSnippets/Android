
# 功能片段



## 连续点击退出应用


```
/**
 * 保存用户按返回键的时间
 */
private long mExitTime = 0;


/**
 * 设置连续点击返回后退出该应用
 */
@Override
public void onBackPressed() {
    if ((System.currentTimeMillis() - mExitTime) > 2000) {
        // 使用Snackbar控件在页面底部进行提示
        Snackbar.make(drawerLayout, "再按一次退出程序哦~", Toast.LENGTH_SHORT).show();
        mExitTime = System.currentTimeMillis();
    } else {
        finish();
    }
}
```








