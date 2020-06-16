## HTTPS
+ HTTPS는 SSL(=TLS) 위에서 돌아가는 프로토콜이다.
+ SSL 디지털 인증서는 '클라이언트 - 서버'간 통신을 제 3자가 보증하기위해 생겼다. 클라이언트가 서버에 접속한 직후, 서버는 클라이언트에게 이 인증서를 전달하며 클라이언트는 이것이 신뢰받는 기관의 것인지 확인한다.
+ SSL에서 사용하는 암호화 방식은 두 가지가 있다.
#### 대칭키
+ 동일한 키로 암호화, 복호화를 모두 처리하는 방식.
#### 공개키
+ 두 개의 키를 가지며 두 키를 A, B라고 가칭하자면 A키로 암호화, B키로 복호화를 하는 방식이다.
+ 두 키 중 하나를 비공개 키, 다른 하나를 공개키로 지정한다. 비공개키는 서버만 가지고있고 공개키를 타인에게 제공한다.
+ 공개키로 암호화한 데이터는 비공개키로 복호화해야하기에 데이터가 탈취되어도 정보를 보호할 수 있다.
+ 반대로 비공개키로 데이터를 암호화하고 공개키로 이를 복호화한다면, 그리고 이 공개키가 신뢰할 수 있는 사이트의 것이라면, 이는 신뢰할 수 있는 정보원으로부터 나온 데이터라 할 수 있다. 이것을 전자서명이라고 한다.
#### SSL 인증서 (비공개 키로 암호화된 인증문서)
+ 공인된 인증서를 발급하는 기관을 CA라고 부른다. 이 인증서들은 브라우저의 소스코드 상에 등록되어있다.
+ 인증서 내에는 서비스의 정보와 서버 측 공개키가 포함된다. 이는 복호화가 잘 되었는지 확인하기 위함이다.
+ 브라우저는 인증서의 발급 CA가 등록된 CA인지 확인한 후, 해당 CA의 공개키를 이용해 인증서를 복호화한다. 복호화가 된다면 인증서는 CA의 비공개키로 암호화됐다는 뜻이며 해당 서버는 신뢰할 수 있다는 뜻이 된다.
#### 동작 방법
+ SSL은 데이터를 보호하기 위해 실제 데이터는 대칭키로, 대칭키는 공개키로 암호화한다.


## CSRF