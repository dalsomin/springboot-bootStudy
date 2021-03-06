@NoArgsContructor를 사용할 때 주의점
 

1. 필드들이 final로 생성되어 있는 경우에는 필드를 초기화 할 수 없기 때문에 생성자를 만들 수 없고 에러가 발생하게 됩니다.

 

이 때는 @NoArgsConstructor(force = true) 옵션을 이용해서 final 필드를 0, false, null 등으로 초기화를 강제로 시켜서 생성자를 만들 수 있습니다.

 

2. @NonNull 같이 필드에 제약조건이 설정되어 있는 경우, 생성자내 null-check 로직이 생성되지 않습니다.

 

후에 초기화를 진행하기 전까지 null-check 로직이 발생하지 않는 점을 염두하고 코드를 개발해야 합니다.

 

@RequiredArgsConstructor
 

이 애노테이션은 추가 작업을 필요로 하는 필드에 대한 생성자를 생성하는 애노테이션입니다.

 

초기화 되지 않은 모든 final 필드, @NonNull로 마크돼있는 모든 필드들에 대한 생성자를 자동으로 생성해줍니다.

 

@NonNull로 마크돼있는 필드들은 null-check가 추가적으로 생성되며, @NonNull이 마크되어 있지만, 파라미터에서 null값이 들어온다면 생성자에서 NullPointerException이 발생합니다.

 

파라미터의 순서는 클래스에 있는 필드 순서에 맞춰서 생성됩니다.
