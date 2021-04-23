# Python Notebook
## 1. numba method
@jit method
@njit method

## 2. Git user 
### 2.1 三大分区
* 工作区，working directory
* 暂存区，stage，index
* 版本库，本地仓库， commit History

### 2.2 *分区转换命令*
* **git add**
数据从工作区转移至暂存区
* **git commit**
代码从暂存区转移至本地仓库，版本库
* **git push**
本地到远程代码库
* **git diff**
工作区与暂存区对比
* **git diff head** 工作区与本地版本库对比
* **git diff --cache** 暂存区、版本库对比
### 2.3 Git初始化

1. git init,初始化一个新的git项目
2.  git config --global user.email "programerhou@outlook.com"
3.  git config --global user.name "houge008"
4.  git cat-file -p 9dae  查看对应文件夹
### 2.4 Git分支
1. tree -a .git  查看git目录树
2. cat .git/refs/heads/master 查看哈希值
3. git branch 创建其他分支 git branch feature/dev
4. git checkout feature/dev  切换分支
5. git branch -vv 
6. git rebas/merge 分支合并
### 2.5 版本回滚
1. git revert 退回上一个commit版本
2. git reset
```
git reset分为三种模式：

    soft
    mixed
    hard
```
```
git rebase 
while(存在冲突) {
    //找到当前冲突文件，编辑解决冲突
    git status
    git add -u
    git rebase --continue
    if( git rebase --abort )
        break; 
}
```
```
$ touch runoob-test.txt      # 添加文件
$ git add runoob-test.txt 
$ git commit -m "添加到远程"
master 69e702d] 添加到远程
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 runoob-test.txt

$ git push origin master    # 推送到 Github
```
H~2~O    x^2^

![Gitexampe](/home/sfa/Pictures/1.jpg)
![Gita](/home/sfa/Pictures/2.jpg)

```
代码行，通过```开启，如果是某种语言，。第一行末尾家还是那个Python,方便加入代码
```
```python
print('hello')
sum = 0
for i in range(100):
    sum += i
return sums 
from functools import wraps

#name output warpper

# def hint(func):
#     def wrapper(*args, **kwargs):
#         print('{} function is running'.format(func.__name__))
#         print('{}.__name__ is:{}'.format(func.__name__,func.__name__))  #hello wrapper
#         return func(*args, **kwargs)
#     return wrapper


# #name output hello
# def hint(func):
#     @wraps(func)
#     def wrapper(*args, **kwargs):
#         print('{} function is running'.format(func.__name__))
#         print('{}.__name__ is:{}'.format(func.__name__,func.__name__))  #hello hello
#         return func(*args, **kwargs)
#     return wrapper

def hint(coder):
    def wrapper(func):
        @wraps(func)
        def inner_wrapper(*args, **kwargs):
            print('{} function is running'.format(func.__name__))
            print('{}.__name__ is:{}'.format(func.__name__,func.__name__))  #hello hello
            print('Coder:{}'.format(coder))
        return inner_wrapper
    return wrapper

'''
前面几个装饰器一般是内外两层嵌套函数。如果我们需要编写的装饰器本身是带参数的，
我们需要编写三层的嵌套函数，其中最外一层用来传递装饰器的参数。
'''

'''
Python的装饰器不仅可以用嵌套函数来编写，还可以使用类来编写。
其调用__init__方法创建实例，传递参数，并调用__call__方法实现对被装饰函数功能的添加。
#类的装饰器写法， 不带参数
class Hint(object):
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print('{} is running'.format(self.func.__name__))
        return self.func(*args, **kwargs)


#类的装饰器写法， 带参数
class Hint(object):
    def __init__(self, coder=None):
        self.coder = coder

    def __call__(self, func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            print('{} is running'.format(func.__name__))
            print('Coder: {}'.format(self.coder))
            return func(*args, **kwargs)     # 正式调用主要处理函数
        return wrapper
'''

# @hint
@hint(coder="Houdj")
def hello():
    print("hello world!")

if __name__ == '__main__':
    hello()
    print('hello.__name__ is:{}'.format(hello.__name__))  #output warpper



'''
值得一提的是被装饰器装饰过的函数看上去名字没变，其实已经变了。当你运行hello()后，
你会发现它的名字已经悄悄变成了wrapper，这显然不是我们想要的.
这一点也不奇怪，因为外函数返回的是由wrapper函数和其外部引用变量组成的闭包。
为了解决这个问题保证装饰过的函数__name__属性不变，
我们可以使用functools模块里的wraps方法，先对func变量进行wraps。
'''
```
