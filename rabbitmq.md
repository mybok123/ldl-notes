### 启动server

> sbin/rabbitmq-server

### 后台启动server

> sbin/rabbitmq-server -detached

### 停止server

> rabbitmqctl stop 

### 查看状态

> rabbitmqctl status 

### 启动网页版控制台

> rabbitmq-plugins enable rabbitmq_management

> http://127.0.0.1:15672/

### 在node中使用 send

```
  var mq_conf = require('../../../config/rabbitmq.js');
  var rabbitmq_connect_str = 'amqp://' + mq_conf.user + ':' + mq_conf.password + '@' + mq_conf.host + '/'; 
  module.exports = function() {
    var url = rabbitmq_connect_str;
    amqp.connect(url, function(err, conn) {
      if (err) {
        return console.log(err)
      };
      conn.createChannel(function(err, chn) {
        if (err) {
          console.log(err);
        };
        var q = 'helloworld1';

        var data = {} ;

        data.name = 'ldl';

        chn.assertQueue(q, {durable: true});
        chn.sendToQueue(q, new Buffer(JSON.stringify(data)));
        chn.ack();
      });
    });
  };
```

### 在node中使用recieve
```
  var mq_conf = require('../../../config/rabbitmq.js');
  var rabbitmq_connect_str = 'amqp://' + mq_conf.user + ':' + mq_conf.password + '@' + mq_conf.host + '/'; 
  var bill_dao = require('@i5ting/hz-dao-billing').bill_dao;
  module.exports = function () {

    amqp.connect(rabbitmq_connect_str, function(err, conn) {
      console.log(err);
      conn.createChannel(function(err, ch) {
        console.log(err);
        var q = 'helloworld1';

        ch.consume(q, function(msg) {
          console.log(msg.content.toString());

          bill_dao.create(JSON.parse(msg.content.toString()));

          ch.ack(msg);
          
        }, {noAck: false});
      });
    });
  }
```