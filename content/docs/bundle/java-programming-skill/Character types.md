
char : 2바이트 사용, 유니코드

문자에 정수 더할 수 있음
아스키코드가 증가됨

String은 정수를 더하면 그냥 더해짐
즉, 문자와 문자열은 반환 구조 자체가 다름

int 로 묵시적 형변환 가능

단, 문자 변수에는 정수 더하지 못함 char 반환 안됨

Character 클래스 사용해서 반환 가능

'1' - '0' 하면 정수 1이 나옴(약간 꼼수)
즉, '0'을 빼주면 해당 숫자 문자의 정수값이 나오게됨

