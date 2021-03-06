#String matching!!

##1. KMP Algorithm

원시적으로 특정 문자열에서 해당 패턴을 모두 찾기 위해선 O(M * N) 의 시간 복잡도가 소요된다.

M = string len , N = pattern len

KMP 알고리즘을 이용하여 O(N+M)에 문자열 검색을 할 수 있다. 즉 패턴의 길이가 짧을 경우, O(N)에 수렴한다.


### KMP 알고리즘이란?
KMP 알고리즘을 만든 사람 이름이 Knuth, Morris, Prett이기 때문에 앞 글자를 하나씩 따서 KMP 알고리즘이라 이름 붙였다. 

### 먼저 알아야 하는 것.

1. 접두사(prefix)와 접미사(suffix)
2. pi배열. p[i]는 주어진 문자열의 0~i 까지의 부분 문자열 중에서 prefix == suffix가 될 수 있는 부분 문자열 중에서 가장 긴 것의 길이 (이때 prefix가 0~i 까지의 부분 문자열과 같으면 안된다.)

무슨 말인지 잘 모를 것이다. 예시를 보고 직관적으로 이해해 보도록 하자.


--


ABAABAB의 pi배열을 구해보자

| i | substring | pi[i] | 
| :--------- | :--------- | :----------: | 
| 0 | A       | 0       | 
| 1 | AB      | 0       | 
| 2 | ABA     | 1       | 
| 3 | ABAA    | 1       |
| 4 | ABAAB   | 2       | 
| 5 | ABAABA  | 3       |
| 6 | ABAABAB | 2       | 

--

한번더 "AABAA"의 pi배열을 구해보자

| i | substring | pi[i] | 
| :--------- | :--------- | :----------: | 
| 0 | A       | 0       | 
| 1 | AA      | 1       | 
| 2 | AAB     | 0       | 
| 3 | AABA    | 1       |
| 4 | AABAA   | 2       | 

###단순한 방법은 정보를 낭비하고 있다.
위에서 설명한 단순한 방법은 진행과정 중에 발생한 멋진 정보를 낭비하고 있다.

어떤 정보를 낭비하고 있는 것일까?

텍스트 " ABCDABCDABDE"에서 패턴 "ABCDABD"를 찾는 상황을 생각해보자.

| index |0 |1 | 2 | 3 | 4 | 5 | 6 | 7 | 8| 9|10|11| 
| :- | :--------- | :------ |  :--------- | :--------- | :----------: |  :--------- | :--------- | :----------|
| 텍스트 | A | B | C | D | A |  B | C | D | A | B | D | E 
| 패턴 | A | B | C| D| A | B | D

| index |0 |1 | 2 | 3 | 4 | 5 | 6 | 7 | 8| 9|10|11| 
| :- | :--------- | :------ |  :--------- | :--------- | :----------: |  :--------- | :--------- | :----------|
| 텍스트 | A | B | C | D | A |  B | C | D | A | B | D | E 
| 패턴 | |A | B | C| D| A | B | D

-> 의미 없음. pi[5] = 2이므로 ..

| index |0 |1 | 2 | 3 | 4 | 5 | 6 | 7 | 8| 9|10|11| 
| :- | :--------- | :------ |  :--------- | :--------- | :----------: |  :--------- | :--------- | :----------|
| 텍스트 | A | B | C | D | A |  B | C | D | A | B | D | E 
| 패턴 | ||||A | B | C| D| A | B | D

-> 여기서 매칭하는 것도 앞에 AB는 굳이 매칭해볼 필요 없음 이미 매칭이 된다는 것을 알고 있기 때문이다.


###KMP의 구현 (C++)

..




more info http://bowbowbow.tistory.com/6