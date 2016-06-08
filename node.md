## 占位符
function sayHi(name) {
  return `How are you, ${name}?`;
}
注意return 后面是` ,tab键上面的输入

## http-server
  说明：是一个简单的web容器 类似于tomcat
  npm install -g http-server
  使用：切换到文件目录，hs启动

## gitbook
> git https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md
> 说明：将markdown文件
> 安装 ：npm install -g gitbook-cli
> 使用 : gitbook serve

### 私有仓库使用 @i5ting/hz-dao-billing

> nrm use npm

> npm login

> npm run dao

> npm start 或 npm publish

> 重新发布 先glup ，将版本号+1

## Promise

> 附 官网api地址 [link](http://bluebirdjs.com/docs/api-reference.html)

### Promise.all()
> Promise.all()
```
var q = [];
 
q.push(
  new Promise(function (resolve,reject) {
    console.log(1);
    setTimeout(function () {
      console.log('1++');
      resolve();
    },2000);
  })
);

q.push(
  new Promise(function (resolve,reject) {
    console.log(2);
    setTimeout(function () {
      console.log('2++');
      resolve();
    },1000);
  })
);

Promise.all(q).then(function () {
  console.log(4);
});

console.log(5);
```
> 输出顺序1、2、5、2++、1++、4
> 其中的两个resolve是必须，否则不能打印4

### Promise.resolve() & Promise.reject()
```
var q = [];

q.push(
  new Promise(function (resolve,reject) {
    console.log(1);
    setTimeout(function () {
      console.log('1++');
      reject('ni shi so ..');
    },2000);
  })
);

q.push(
  new Promise(function (resolve,reject) {
    console.log(2);
    setTimeout(function () {
      console.log('2++');
      resolve();
    },1000);
  })
);

Promise.all(q).then(function () {
  console.log(4);
})
.catch(function (err) {
  console.log(err);
});

console.log(5);
```

> 输出值为1、2、5、2++、1++、ni shi so ..




