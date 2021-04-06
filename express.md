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
  > **use�޼���**�� **��� HTTP �޼���**�� ���� ��û �ּҸ� ��ġ�ϸ� ��������� **get, post, put, patch, delete** ���� �޼���� **�ּһӸ� �ƴ϶� HTTP �޼������ ��ġ �ϴ� ��û**�� ���� ����   
  
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
  
   + next('route')
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