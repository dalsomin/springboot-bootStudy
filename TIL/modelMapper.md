이번에는 java에서 내가 애용하는 modelMapper에 관해 글을 써보고자 한다. 엄청 유용한 라이브러리임에도 불구하고, 그래서 java 사용자는 모두들 사용하고 있을거라고 생각했는데, 생각보다 주위에 물어봤을때 ‘처음 듣는다. modelMapper가 뭐에요?’ 하는 반응이 꽤 있어서, 이미 많은 사람들이 소개 했지만, 공부도 할겸 나도 한번 소개해 보고자 한다.

야 너두 짤에 대한 이미지 검색결과
사실 나도 얼마전까진 몰랐다..
아래 나오는 코드들은 Java 1.8 이상을 기준으로 한다. Java 1.6/1.7 은 사용 가능하나, 아래 코드와는 약간 코드 스타일이 다르다. 가이드는 공식 홈페이지에서 확인 바람

2.3.0 기준으로 JAVA 11도 지원한다.
ModelMapper, 무엇?
“Intelligent object mapping” – ModelMapper github

지능적인 object mapping이다.

“서로 다른 클래스의 값을 한번에 복사하게 도와주는 라이브러리”

한줄로 요약하자면 위와 같다. 말 그대로, 다른 클래스로 어떠한 object가 갖고 있는 필드 값들을 쉽게, 자동으로 mapping 해주는 라이브러리다. #링크 – 공식 사이트

대부분의 필드들, 이름과 자료형이 같다면 getter, setter를 통해 자동으로 값을 복사해 주거나, 복사한 object를 만들어 주며, 완전히 동일하지 않더라도 규칙 설정을 통해 자동으로 매핑하도록 할수도 있고, 완전 다른 경우에는 커스터마이징을 통해 각 필드별로 수동으로 매핑 설정을 해줄 수도 있다.

👓왜 써야하죠?
1. 귀찮으니까

2. 실수를 줄이기 위해

가장 큰 이유는 귀찮으니까 쓴다. 웹 어플리케이션 뿐만 아니라, input과 output과 repository에 저장되는 data의 모델링이 다른 경우가 많고, 그렇다면 결국 다른 모델의 object를 변환해줘야 하는 작업이 빈번하게 발생한다.

필드 한두개 쯤이야, 그냥 get/set 으로 쓰겠지만, 어디 우리가 하는 일이 그러한가? 20개쯤은 되어 줘야 일 하는 느낌이 들지.. 이렇게 get/set으로 노가다 매핑을 반복하다 보면, 빼먹는 필드들 한두개쯤 자연스레 생기고, 침침한 눈으로 눈알 빠지게 어느 필드 빼먹었나 찾아보게 되는 상황이 발생한다.

자동으로 매핑하면 이런 실수를 줄일 수 있게 도와준다. (물론 그렇다고 실수를 안하는건 아니지만… 약간 실수 질량보존의 법칙 같은건가? 여기서 빵꾸 안내면 다른데서 어디서든 빵꾸 내더라.)

언제 써야 하죠❓
예를 들어, 내가 회사에서 진행하는 프로젝트에서, view layer에서 사용하는 data의 형태는 dto라고 이름 붙여서 사용하는데, 이는 repository에서 사용하는 entity class 형태와 필드 대부분은 동일하나, 다른 형태로 구성되어 있다. 결국 repository에서 불러온 entity object는 dto 형태로 매핑해서 controller를 통해 응답하게 되고, 반대로 put이나 post 같은 경우, controller에서 받은 dto object를 entity 형태로 변환해야 한다.

이렇게 get/set 를 통해 object 를 다른 형태로 변환할때, 이게 귀찮아서 더이상 일일히 손으로 하기 싫을때 쓰면 된다.

modelMapper를 모르던 시절이 있었다. 그때는, “아.. 이런 작업을 줄일수는 없을까?” 고민하다가 reflection api를 활용해서 매핑해주는 유틸리티를 직접 만들어서 써보기도 했다. getter/setter 에서 field 이름을 추출하고, 일치하면 invoke 해서 값 넣어주는..
