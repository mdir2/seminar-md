# 더 자바 by 백기선
## 코드를 테스트하는 다양한 방법 
> __선행 :__ 코드를 조작하는 방법 in 인프런
### Junit 5
* 빈티지 의존을 추가하면 Junit 4로 작성한 테스트 코드도 돌릴 수 있음.
* @DisplayName : 논리적으로 메소드 이름을 정해줘서 명시적으로 볼 수 있게 해줌.
    * scope : class, method
* 전체 validation 하는 방법
```java
assertAll(
    () -> something
    () -> something
    ...
);
```
> __Note :__ assert*(expected, actual, message);

* throw 변경
```java
@Test(exception bla bla) --> assertThrow()
```

* @TestInstance(LifeCycle.PER_CLASS) : 테스트 클래스의 인스턴스를 단일 인스턴스로 바꿔 줌

* @SpringBootTest에 @ExtentionWith에서 @RunWith 역할을 해줌 그래서 생략 해도 됨.

* 위에 상황에서 발생되는 혼란을 위해서 빈티지 의존성을 제외하는 것이 맞아 보임.

### Mockito
* @ExtendWith(MockitoExcetion.class)
* Stubbing ; mock 객체 동작 로직에 대한 명세
    * Given --> When --> Then

#### 슬라이스 테스트 --> 통합 테스트
> 테스트환경과 프로덕션 환경의 갭을 줄이기 위함
* 레파지토리 모킹은 안함 --> 테스트용 디비를 띄움 --> 대신에 번거로움
* @TestContainers로 번거로움 해소 가능
    * @Container : DB에만 국한 되는 것이 아니라 어떠한 도커 이미지라도 테스트용 컨테이너로 띄울 수 있음
* 서비스도 컨테이너로 관리 가능
    * Docker Compose 이용
    * 작성한 compose 파일을 가지고도 테스트가능
        * 따로 Docker Compose를 띄울 필요가 없음.

* JUnit5의 @Tag 로 CI, CD 서버에서 돌때와 개발환경에서 돌때를 구분하게 해서 돌리면 느리다는 단점을 보완 할 수 도 있음

* 장애사항을 재현할수있는 
```
Chaos Monkey
```

> __Note :__ @RequiredArgsContructor 인스턴스 변수를 아규먼트로 받는 생성자를 자동으로 만들어줌