Node.JS Express
===============

�����
------

  * Ŭ���̾�Ʈ���� ������ �ּҿ� ���� �ٸ� ó���� �ϴ� ���� �ǹ�   
  * �⺻ ����: app[REST�޼ҵ�]('�ּ�', �ݹ��Լ�)   
  > Rest�޼ҵ�: use, get, post, put, delete  
  <pre><code>
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
  </code></pre>   
  > **use�޼���**�� **��� HTTP �޼���**�� ���� ��û �ּҸ� ��ġ�ϸ� ���������,   
   **get, post, put, patch, delete** ���� �޼���� **�ּһӸ� �ƴ϶� HTTP �޼������ ��ġ �ϴ� ��û**�� ���� ����   
  
  * �ּ� �κ��� ���� ǥ���ĵ� �����ϰ� :(�ݷ�)�� ����� ���ϵ�ī�嵵 ����   
  <pre><code>
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID)
  });
  </code></pre>   
  
  * ������ �߿���   
  <pre><code>
  // ���� ��� �Ʒ��� ���� �ڵ忡�� ������ ����ǰ� �Ʒ��� ������ �ȵ�
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID + 'ù��°') // �����
  });
  
  app.get('/page/a', (req, res) => {
    res.send(req.params.pageID + '�ι�°') // �ȵ�
  });
  </code></pre>  
  
  * �ݹ��Լ� �⺻ ����: request, response, next   
  <pre><code>
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID + 'ù��°') // �����
  });
  </code></pre>  
  * request   
    - params: ����� �Ķ���͸� ����   
    - query: GET ������� �Ѿ���� ���� ��Ʈ�� �Ķ���͸� ����   
    - body: POST ������� �Ѿ���� �Ķ���͸� ����   
      + �Ľ��� ���ؼ��� body-parser�� ���� �̵���� �ʿ�   
    - ... ����   
  <pre><code>
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
  </code></pre>  
  > body-parser
  <pre><code>
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
  </code></pre>  
  * response   
    - send: �⺻���� ���� �޼���   
    - sendFile: ������ �������� ����   
    - json: Json ����  
    - redirect: ������ �ٸ� ����ͷ� ����   
    - ... ����   
  <pre><code>
  app.get('/redirectTest', (req, res) => {
    res.redirect('/'); // Ȩ ȣ��
  });
  </code></pre>  
  
  * next   
    + ���� ����Ϳ��� �Ǵ����� �ʰ� ���� ����ͷ� �ѱ�� ����
 <pre><code>
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
  </code></pre>
  
  * next('route')   
    - ����Ϳ� ����� ������ �̵������� �ǳʶٰ� ���� �� ���
      
<pre><code>
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
</code></pre>  
  
   > **route�� �ٸ� �Ű����� ���޽� error�� ��**   
   <pre><code>
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
  </code></pre>  