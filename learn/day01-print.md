# print函数
- python3中需要在print后加括号，如:print('')    ||python2中不需要
- 一般使用方法为: print('hello')  || print('hello','word')  效果相同
- 升阶的参数为  sep  end  file ，其中sep默认为空，end默认为\n，file为文本编辑
``` 
print('hello','word',sep=' ',end='\n') 效果等同print('hello','word') 
```
```
with open('a,txt','w')as f:
  print("file\n","abc","fff",sep='#########\n',end='',file=f)
```
> 链接：https://blog.csdn.net/asdfg34rt/article/details/80712031
可以利用end和file的函数消除文件中换行符
