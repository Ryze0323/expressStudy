Node.JS Express
===============

�����
------

  * Ŭ���̾�Ʈ���� ������ �ּҿ� ���� �ٸ� ó���� �ϴ� ���� �ǹ�   
  * �⺻ ����: app[REST�޼ҵ�]('�ּ�', �ݹ��Լ�)   
  Rest�޼ҵ忡�� get, post, put,delete�� ����   
  <pre><code>
  app.get('/', (req, res) => {});
  </code></pre>   
  
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
  
  