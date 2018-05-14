# test
Flask
微框架

django——完善完整高集成的框架
flask——不包含数据，框架，抽象库，等，需要自己去配置

安装：
1.虚拟环境 
2.安装flask
pip install flask
3.写入：
from flask import Flask

# 初始化，--name--代表主模块名或者包
app = Flask(__name__)
# 路由
@app.route('/')
def hello():
    # 视图函数
    return 'HELLO,world'
if __name__ == '__main__':
    # 启动
    app.run(debug=True) 
4.运行
python xx.py 默认127.0.0.1：5000端口

run里面有参数：
debug=True 这样可以将错误显示在浏览器中
port='自己端口号' 修改端口号
host = '0.0.0.0' 都可以访问 ip

修改动态参数
app中传入<>,然后def中引用
# 动态传入url参数
@app.route('/he/<name>/')
def he(name):
    # 传入的name为字符串
    print(name)
    return 'hello %s' % name

*传入的为str类型

*如果需要指定传入int类型<int:name>
# 修改后只能传入数字，否则报错
@app.route('/hello/<int:name>/')
def hello_int(name):
    # 传入的name为整数
    print(name)
    return 'hello %s' % name

修改启动方式：
修改成类似django的用法
1.安装
pip install Flsak-Script
2.配置
manager = Manager(app=app)
启动改为
manager.run()
这样启动的时候就是
python xxx.py runserver -p（端口号） -h（IP） -d（debug模式）

蓝图(用来管理url)
将url、启动和方法从一个py文件分离开
pip install flask-blueprint
1.初始化
单独创建一个文件写入，url和views方法的
from flask import Blueprint

blue = Blueprint('first', __name__)
把@app改成@blue
@blue.route('/')
def hello():
    # 视图函数
    return 'HELLO,world'
2.路由注册
在该文件下创建init文件
图1
def xx（）:
app = Flask(__name__)
    app.register_blueprint(blueprint=blue)
    return app

然后启动页面——可以改成manage。py：
blue = xx()
manager = Manager(app=blue)


参数规则

默认string类型
可以用int，float等
path：/也是当做字符串返回
@blue.route('/getpath/<path:ff>')
图2
uuid 返回的是一个随机的很长的字符串
图3