# 유니코드와 텍스트 인코딩 인트로

유니코드란 무엇인가? 유니코드는 전세계 거의 모든 글자를 포함한 맵핑 시스템이며 Unicode Consortium 이라는 비영리단체가 운영하고 있다.
[위키 출처](https://en.wikipedia.org/wiki/Unicode)

세계 각국 언어문자 및 자주쓰는 특수 문자와 심볼들이 U+0000 에서 U+FFFF 형태로 맵핑이 되어 있으며 이 범위에 있는 유니코드를 Basic 또는 Plane 0 라고한다. Basic 에 포함되어있는 유니코드 가지수는 2의 16승 또는 65536개 이다.

하지만 일부 중국문자와 아주 다양한 이모티콘 같이 언어가 아닌 문자들까지 포함시키기 위해 Plane 을 계속 추가하고 있으며
예를들어서

Plane 1 은 U+10000 에서 U+1FFFF,
Plane 2 는 U+20000 에서 U+2FFFF 이다.

현재 Plane 16 까지 정의되어 있으며, 범위는 U+100000 에서 U+10FFFF이다.
Plane 0 은 Basic 이라고 불리며 Plane 1 부터 16은 Supplementary 라고 부른다.

예를들어 Capital letter J 는 유니코드로 U+004A 이고, [출처](https://en.wikipedia.org/wiki/List_of_Unicode_characters)
한글 기역 ㄱ 은 U+3131 이며 [출처](https://www.learnkoreantools.com/en/korean-to-unicode)
중국 中 은 U+4E2D 이고 [출처](https://www.unicode.org/cgi-bin/GetUnihanData.pl?codepoint=%E4%B8%AD)
이모티콘 😀 은 U+1F600 이다 (Supplementary / Plane 1). [출처](https://unicode.org/emoji/charts/full-emoji-list.html)

세계 언어문자들은 일부 중국 한자만 제외하고 거의다 Plane 0에 포함이 되어 있다.

(참조: 한글은 가각간 에서 시작해서 히힣 까지 각자 새로운 유니코드를 가지고있고 추가적으로 ㄱㄴㄷㄹ ㅣ ㅢ 와 같은 자음 모음도 유니코드에 들어있다.)

유니코드를 간단하게 비유하자면 단순히 숫자와 문자를 1대1로 연결해주는 사전같은 것이다.

## 인코딩이 무엇인가? [위키 출처](https://en.wikipedia.org/wiki/Character_encoding)

인코딩이랑 컴퓨터가 사람이 쓰는 문자를 숫자로 변환하여 다른 컴퓨터와 대화할수있도록 하는 방식이며, 디코딩이란 이 숫자를 다시 문자로 변환해주는것을 의미한다. (컴퓨터는 0하고 1만 주고받을수있다).

현재 세계적으로 가장 많이 쓰이는 UTF-8 은 Unicode 를 활용한 인코딩이다.
[utf-8 출처](https://en.wikipedia.org/wiki/UTF-8)

utf-8 같은경우 variable-width character encoding 의 한 종류다. utf-8 은 총 1,112,064 의 문자를 표현할수 있으며, 자주 쓰는 문자는 1바이트, 그다음은 2바이트, 그다음은 3바이트, 그다음은 4바이트등 문자마다 쓰는 바이트 용량이 다르다.

1~4바이트중 몇 바이트를 쓰는지는 앞에 오는 바이너리 코드를 보면 알수 있다.
0xxxxxxx 는 1바이트
110xxxxx 10xxxxxx 는 2바이트
1110xxxx 10xxxxxx 10xxxxxx 는 3바이트
11110xxx 10xxxxxx 10xxxxxx 10xxxxxx 는 4바이트이다.

utf-8 에서 1바이트의 범위는 00000000 에서 011111111 이며 유니코드로 볼때는 U+0000 에서 U+007F 이다.

즉 위에서 말한 Capital letter J (U+004A)
는 utf-8 에서는 그대로 01001010 이고,

2바이트는 유니코드 범위로 볼때 U+0080 U+07FF 이며
3바이트는 U+0800 U+FFFF
4바이트는 U+10000 U+10FFFF
이다.

한글, 일본, 그리고 대부분의 중국어 같은 경우 유니코드 3바이트 범위에 들어간다.
한글 ㄱ 은 U+3131 이며 이것을 바이너리로 변경하면.
0011 000100 110001 이다.

zzzz yyyyyy xxxxxx

이것을 1110zzzz 10yyyyyy 10xxxxxx

이런식으로 끼워 넣으면.

1110**0011** 10**000100** 10**110001** 인것이다.

즉 한글 ㄱ 은 utf-8에서는 위 바이너리로 인코딩되고 핵스값은 E384B1 이다.
