Node.JS Express
===============

라우팅
------

  * 클라이언트에서 보내는 주소에 따라 다른 처리를 하는 것을 의미   
  * 기본 사용법: app[REST메소드]('주소', 콜백함수)   
  <pre><code>
  app.get('/', (req, res) => {});
  </code></pre>   
  * 주소 부분은 정규 표현식도 가능하고 :(콜론)을 사용한 와일드카드도 가능   
  <pre><code>
  app.get('/page/:pageID', (req, res) => {
    res.send(req.params.pageID)
  });
  </code></pre>   
  * 순서도 중요함   