# `UIInput.open()`回调函数的兼容性问题
``` bash
# 回调函数参数 ret.id 存在兼容性问题，苹果系统从 1 开始，安卓系统从 0 开始。
# 所以：想要使用 ret.id 来判断是哪一个输入框的输入值是不好的。
UIInput.open({}, ret => {
  UIInput.value({ id: ret.id }, value => {
    alert(value.msg)
  })
})

```

# 阻止返回上一个界面
``` bash
# 安卓系统监听按返回键的事件即可阻止返回上一个界面，ios无此事件
api.addEventListener({ name: 'keyback' }, (ret, err) => { });

# ios 需要在打开win时，配置选项 slidBackEnabled: false,安卓无效
api.openWin({
  name: 'login_win',
  url: 'html/login_win.html',
  slidBackEnabled: false, # 生效配置
});
api.openDrawerLayout({
  name: 'home_win',
  url: 'html/home_win.html',
  slidBackEnabled: false, # 生效配置
  leftPane: {
    name: 'userinfo_win',
    url: 'html/userinfo_win.html',
    bounces:false,
  }
});
```
# icon包含全部内容： background-size: contain;background-position: center;

# 背景大图，覆盖完所有区域： background-size: cover;
#并且如果有输入框应该使用，background-position: top;安卓手机弹出输入框背景才不会移动位置
