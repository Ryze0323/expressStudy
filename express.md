Node.JS Express
===============

라우팅
------

  * 클라이언트에서 보내는 주소에 따라 다른 처리를 하는 것을 의미   
  * 기본 사용법: app[REST메소드]('주소', 콜백함수)   
  > Rest메소드: use, get, post, put, delete  
  <pre><code>
  app.use('/',function(req,res,next){
    console.log('/ 주소의 요청일 때 실행된다.');
    res.send('주소의 요청일 때 실행된다.');
    next();
  });

  app.get('/',function(req,res,next){
      console.log('GET 메서드 / 주소의 요청일 때만 실행 된다.');
      res.send('GET 메서드 / 주소의 요청일 때만 실행 된다.');
      next();
  });

  app.post('/data',function(req,res,next){
      console.log('POST 메서드 / data 주소의 요청일 때만 실행된다.');
      res.send('POST 메서드 / data 주소의 요청일 때만 실행된다.');
      next();
  });
  </code></pre>   
  > **use메서드**는 **모든 HTTP 메서드**에 대해 요청 주소만 일치하면 실행되지만 **get, post, put, patch, delete** 같은 메서드는 **주소뿐만 아니라 HTTP 메서드까지 일치 하는 요청**일 때만 실행   
  
  * 주소 부분은 정규 표현식도 가능하고 :(콜론)을 사용한 와일드카드도 가능   
  <pre><code>
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID)
  });
  </code></pre>   
  
  * 순서도 중요함   
  <pre><code>
  // 예를 들어 아래와 같은 코드에서 위에만 실행되고 아래는 실행이 안됨
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID + '첫번째') // 실행됨
  });
  
  app.get('/page/a', (req, res) => {
    res.send(req.params.pageID + '두번째') // 안됨
  });
  </code></pre>  
  
  * next   
   + 현재 라우터에서 판단하지 않고 다음 라우터로 넘기는 행위
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
    - 라우터에 연결된 나머지 미들웨어들을 건너뛰고 싶을 때 사용   
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
  
   > **route외 다른 매개변수 전달시 error로 감**   
   <pre><code>
   app.get('/', function(req,res,next){
      console.log('0');
      next('test입니다.');
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