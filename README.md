# A37App
个人财务管理app

# 设计文档的关键字
table : 这是数据库中的表
page : 这是设计app的页面名字
field : 表中的字段

# 命名统一：
for table : 使用下划线分割的所有字母大写的单词命名
for field : 同table
for page ：用下划线分割的小写单词命名，注意，这应当同时也是页面文件的命名
for 所有变量 : 用下划线分割的小写单词命名 register_button 等，包括控件名，当然，我们允许单个单词变量存在，但是原则上这些变量应该是局部的
for 所有函数 : 用驼峰命名法 例如 isLogined()  getHashPwd() ....等

TIPs:如果英文不好去CODELF网站上输入中文意思会自动给弹出推荐命名

# 数据库
以下是数据库部分，注意到命名全部是大写字母，这是为了更好的区分原始数据（即数据库请求内容）和其他类型（临时变量等）

## table USER_KEYINFO_TABLE (用户关键登陆信息)
1.  UUID type: INT(?) 
来唯一确定一个用户  
UUID = (wxuuid or alipayuuid or time) *31993 再取后n位   
2.  HASH_PWD   type: VARCHAR(100)
哈希加密过的password 

## table USER_INFO_TABLE (用户基础信息)
1. UUID :主键 见用户登陆信息表
2. BIRTH_DAY type: DATE
记录用户出生日期 
3. NICKNAME type: varchar(100) 账户名字 
4. PHONE_NUMBER : INT(13)
实际为11位数

## 额外注释： 
PHONE_NUMBER 强制要求，注册时必须要有，不可为null
UUID : 通过注册时间或wechat UUID 或alipay UUid生成  
NICKNAME :后期用户可以自己改，默认是等于account birthday 出生日期，不可为空，注册时必须有 ## table  用户收支表

# 页面
## page register_page (注册页面)
输入信息: 姓名(NICK_NAME) 和 手机号(PHONE_NUMBER)
要求交互: 
1.短信验证手机号
2.密码,以及确认密码  
3.生日要求必填

通常使用微信支付宝登陆 （无法直接获得手机号)

按钮控件:
1. submit
2. wechat_register
3. alipay register
必须要在微信或支付宝完成一个绑定后才能submit

完整流程：
一.
1.用户输入手机号密码，检测其合法性  
  密码标准格式要求 1. 字母(大小写都要) 2. 数字3.大于6位
  手机号则检测是否为11位
2.用户输入确认密码，检测是否一致
3.是否

# module 登录注册模块
## page login_page  (登陆页面)
控件
1.phonenumber_input (input框)
2.password_input (input框)
3.login_input (button)
4.forgetpwd_input 忘记密码(button)
5.message_auth_input 短信登陆(button):在忘记密码边上
6.wechat_login_button 微信登陆
7.alipay_login_button 支付宝登陆
8.return_button 返回按钮

## page forget_pwd_page 
忘记密码后的密码界面
2.phonenumber 手机号码
3.短信验证框(input框)

## page user_info_page
用户信息界面 
我们需要展示以下信息
1. nickname
2. phonenumber （需要提供解绑按钮)但是解绑必须使用另外一个手机号验证后代替
3. alipay 是否已经绑定
4. wechat 是否已经绑定
## page initial_page  
这是用户一开始打开app就看到的页面，我们希望每次点开页面都需要进行登陆而不是依靠缓存
