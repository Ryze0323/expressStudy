Node.JS Express
===============
Express
------
NodeJS�� ����Ͽ� ������ �����ϰ��� �ϴ� �����ڵ��� ���Ͽ� ������ ���� ������ �� �ְ� ���� �����ӿ�ũ


�����
------

  * Ŭ���̾�Ʈ���� ������ �ּҿ� ���� �ٸ� ó���� �ϴ� ���� �ǹ�   
  * �⺻ ����: app[REST�޼ҵ�]('�ּ�', �ݹ��Լ�, �ݹ��Լ�, �ݹ��Լ�....)   
  > Rest�޼ҵ�: use, get, post, put, delete  
  ```javaScript
  app.use('/',function(req,res,next){
    console.log('/ �ּ��� ��û�� �� ����ȴ�.');
    res.send('�ּ��� ��û�� �� ����ȴ�.');
    next();
  });

  app.get('/',function(req,res,next){
    console.log('GET �޼��� / �ּ��� ��û�� ���� ���� �ȴ�.');
    res.send('GET �޼��� / �ּ��� ��û�� ���� ���� �ȴ�.');
    next();
  });

  app.post('/data',function(req,res,next){
    console.log('POST �޼��� / data �ּ��� ��û�� ���� ����ȴ�.');
    res.send('POST �޼��� / data �ּ��� ��û�� ���� ����ȴ�.');
    next();
  });
  ```
  > **use�޼���**�� **��� HTTP �޼���**�� ���� ��û �ּҸ� ��ġ�ϸ� ���������,   
   **get, post, put, patch, delete** ���� �޼���� **�ּһӸ� �ƴ϶� HTTP �޼������ ��ġ �ϴ� ��û**�� ���� ����   
  
  * �ּ� �κ��� ���� ǥ���ĵ� �����ϰ� :(�ݷ�)�� ����� ���ϵ�ī�嵵 ����   
  ```javaScript
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID)
  });
  ``` 
  
  * ������ �߿���   
  ```javaScript
  // ���� ��� �Ʒ��� ���� �ڵ忡�� ������ ����ǰ� �Ʒ��� ������ �ȵ�
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID + 'ù��°') // �����
  });
  
  app.get('/page/a', (req, res) => {
    res.send(req.params.pageID + '�ι�°') // �ȵ�
  });
  ```
  
  * �ݹ��Լ� �⺻ ����: request, response, next   
  ```javaScript
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID + 'ù��°') // �����
  });
  ```
  * request   
    - params: ����� �Ķ���͸� ����   
    - query: GET ������� �Ѿ���� ���� ��Ʈ�� �Ķ���͸� ����   
    - body: POST ������� �Ѿ���� �Ķ���͸� ����   
      + �Ľ��� ���ؼ��� body-parser�� ���� �̵���� �ʿ�   
    - ... ����   
  ```javaScript
const qs = require('querystring');
app.get('/', (req, res) => {
    let body = '';
    req.on('data', function(data){
        body = body + data;
    });
    req.on('end', function(){
      body = qs.parse(body)
      let reSend = `params: ${JSON.stringify(req.params)},
      query: ${JSON.stringify(req.query)},
      body: ${JSON.stringify(body)}`
      let html =`
        ${reSend}
        <form action="/" method="post">
          <input type="text" name="post" />
          <p>
            <input type="submit" value="POST TEST">
          </p>
        </form>
      `
      res.send(html);
    });
});

app.post('/', (req, res) => {
    let body = '';
    req.on('data', function(data){
        body = body + data;
    });
    req.on('end', function(){
      body = qs.parse(body)
      let reSend = `params: ${JSON.stringify(req.params)},
      query: ${JSON.stringify(req.query)},
      body: ${JSON.stringify(body)}`
      let html =`
        ${reSend}
        <form action="/" method="get">
          <input type="text" name="get" />
          <p>
            <input type="submit" value="GET TEST">
          </p>
        </form>
      `
      res.send(html);
    });
});
  ```
  > body-parser
  ```javaScript
  const bodyParser = require('body-parser');
  app.use(bodyParser.urlencoded({ extended: false }));
  app.get('/', (req, res) => {
    let reSend = `params: ${JSON.stringify(req.params)},
    query: ${JSON.stringify(req.query)},
    body: ${JSON.stringify(req.body)}`
    let html =`
      ${reSend}
      <form action="/" method="post">
        <input type="text" name="post" />
        <p>
          <input type="submit" value="POST TEST">
        </p>
      </form>
    `
    res.send(html);
  });
  app.post('/', (req, res) => {
    let reSend = `params: ${JSON.stringify(req.params)},
    query: ${JSON.stringify(req.query)},
    body: ${JSON.stringify(req.body)}`
    let html =`
      ${reSend}
      <form action="/" method="get">
        <input type="text" name="get" />
        <p>
          <input type="submit" value="GET TEST">
        </p>
      </form>
    `
    res.send(html);
  });
  ``` 
  * response   
    - send: �⺻���� ���� �޼���   
    - sendFile: ������ �������� ����   
    - json: Json ����  
    - redirect: ������ �ٸ� ����ͷ� ����   
    - ... ����   
  ```javaScript
  app.get('/redirectTest', (req, res) => {
    res.redirect('/'); // Ȩ ȣ��
  });
  ```  
  
  * next   
    + ���� ����Ϳ��� �Ǵ����� �ʰ� ���� ����ͷ� �ѱ�� ����
 ```javaScript
 app.get('/', function(req,res,next){
    console.log('0');
    next();
  },function(req,res,next){
      console.log('1');
      next();
  },function(req,res,next){
      next();
      console.log('2');
  });
   
  app.get('/',function(req,res){
      console.log('3');
  })
  ```
  
  * next('route')   
    - ����Ϳ� ����� ������ �̵������� �ǳʶٰ� ���� �� ���
      
  ```javaScript
  app.get('/', function(req,res,next){
    console.log('0');
    next('route');
  },function(req,res,next){
      console.log('1');
      next();
  },function(req,res,next){
      next();
      console.log('2');
  });
   
  app.get('/',function(req,res){
      console.log('3');
  })
  ```
  
   > **route�� �ٸ� �Ű����� ���޽� error�� ��**   
  ```javaScript
  app.get('/', function(req,res,next){
    console.log('0');
    next('test�Դϴ�.');
  },function(req,res,next){
      console.log('1');
      next();
  },function(req,res,next){
      next();
      console.log('2');
  });
   
  app.use(function(err, req, res, next) {
    res.status(500).send(err);
  })
  ```
  
�̵����
-------
��û�� ������ �߰�(middle, �̵�)�� ��ġ�Ͽ� �̵����� �Ҹ�   
�̵����� �ַ� app.use�� �Բ� ���
```javaScript
app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
```
app.use �޼����� ���ڷ� ��� �ִ� �Լ��� �̵������   
   
> ����   
   
![ex_screenshot](./img/�̵����.jpg)