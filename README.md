# PracticeLab0
---   

⚠️ 본 실습은 포큐수강생이 만든 포큐아카데미의 실습,과제들을 체험할 수 있는 비공식 실습문서입니다. ⚠️   
참조: https://pocu.academy/ko/Policies/Terms

---   

실습0은 실습1을 쉽사리 끝내고 동영상 강의도 3주치를 당겨서 들어버려서 심심하실 분들을 위해 만든 과제입니다.
COMP1500을 들으셨다면 C#기능의 일부분도 복습한다고 생각하시면 좋아요 :)

---   

순환소수(循環小數, repeating decimal 또는 recurring decimal)는 소수점 아래의 어떤 자리에서부터 0이 아닌 일정한 숫자의 배열이 계속해서 되풀이 되는 무한소수를 말합니다. 예시로는 0.1111... 이나 0.16666... 과 같은 소수들이 있습니다.   

순환마디(repetend)는 순환소수에서 일정하게 되풀이 되는 한 부분을 말합니다. 단, 순환마디 길이는 최소여야 합니다.
예를 들면 0.3333... 의 순환마디는 3 입니다.   

여러분이 해야할 일은 어떤 분수가 순환소수인지 아닌지 판단하고 입력받은 분수를 소수로 만드는 함수와 입력받은 소수를 다시 분수로 바꾸는 함수를 작성하는 것입니다.   

---
 <br/>
 <br/>  
 
### 1. 프로젝트를 준비합니다   

 1. 실습문서의 `Clone or download` 버튼 클릭 > `Download ZIP` 선택하여 압축파일을 다운 받고 풀어줍니다.
![chrome_6nQQ8pQZGf](https://user-images.githubusercontent.com/70578707/131924269-4cbff23e-d4dc-438f-978a-09af58d6d6ff.png)   
<br/>

 2. `Lab0.cs` 파일에 다음과 같은 코드가 작성되어있습니다. 
```C#
namespace lab0
{
    public static class Lab0
    {
        public static bool TryGetRepeatingDecimal(int numerator, int denominator, out string stringDecimal)
        {
            stringDecimal= "sample";

            return false;
        }
				
	public static bool TryGetIrreducibleFraction(string stringDecimal, out string irreducibleFraction)
	{
	    irreducibleFraction = "sample";
			
	    return false;
	}
    }
}
```   

---
<br/><br/>

## 2. `Lab0.cs` 안에 함수 구현하기
### 2.1 `TryGetRepeatingDecimal()` 함수 구현하기
- `TryGetRepeatingDecimal()` 함수는 `int numerator`, `int donominator` 인자와 `out stirng stringDecimal` 을 out매개변수로 받습니다.
- 분자를 분모로 나눈 값이 순환소수로 표현되면 `True` 를 반환하고 순환소수로 표현되지 않는다면 `False`를 반환합니다.
- out매개변수인 `stringDecimal`에는 분수에서 변환된 소수를 저장합니다.
- 변환된 소수가 순환소수일 경우 순환마디의 끝과 시작에 `*` 를 붙입니다.    
     ex)  0.0909090909... → 0.0&#42;90&#42;   
          0.2222222222... → 0.&#42;2&#42;   

- 분자의 범위는 0 이상의 양수입니다. 범위를 넘어서면 `False`를 반환합니다.
- 분모의 범위는 0 이상 100이하입니다. 범위를 넘어서면 `False`를 반환합니다.
- `False`값을 반환하면 빈 문자열을 `stringDecimal`에 저장합니다.   
  
<br/>

이 함수를 사용하는 방법은 다음과 같습니다
```C#

  string stringDecimal;

  bool bResult1 = Lab0.TryGetRepeatingDecimal(0, 1, out stringDecimal); // False, "0"
  bool bResult2 = Lab0.TryGetRepeatingDecimal(1, 3, out stringDecimal); // True, "0.*3*"
  bool bResult3 = Lab0.TryGetRepeatingDecimal(1, 4, out stringDecimal); // false, "0.25"
  bool bResult4 = Lab0.TryGetRepeatingDecimal(2, 9, out stringDecimal); // True, "0.*2*"
  bool bResult5 = Lab0.TryGetRepeatingDecimal(1, -3, out stringDecimal); // False, ""

```   
<br/><br/>

### 2.2 `TryGetIrreducibleFraction()` 함수 구현하기
- `TryGetIrreducibleFraction()` 함수는 `string stringDecimal` 인자와 out매개변수 `out string irreducibleFraction` 을 인자로 받습니다.
- 입력받은 `stringDecimal`을 기약분수 꼴로 표현할 수 있다면 `true`, 아니라면 `false`를 반환합니다.
- 결과값이 `false` 라면 `irreducibleFraction` 에 빈 문자열을 저장합니다.
- 기약분수로 표현한다는 의미: x / y 꼴로 표현할 수 있어야 함(x,y 는 서로소인 정수)

     ex) 0.1    →  1 / 10  
         0.&#42;3&#42;  →  1 / 3  

- `string stringDecimal` 로 들어올 수 있는 값은 `TryGetRepeatingDecimal()`함수의 out매개변수로 만들어진 `stringDecimal`값 중 1 미만의 값과 같다고 전제하셔도 됩니다.
- `long` 자료형을 사용하시면 안 됩니다. `int`형만 사용하세요!   
<br/>

이 함수를 사용하는 방법은 다음과 같습니다
```C#
  string irreducibleFraction;
            
  bool bResult6 = Lab0.TryGetIrreducibleFraction("0.13", out irreducibleFraction); // True, "13 / 100"
  bool bResult7 = Lab0.TryGetIrreducibleFraction("0.1*6*", out irreducibleFraction); // True, "1 / 6"
  bool bResult8 = Lab0.TryGetIrreducibleFraction("0.25", out irreducibleFraction); // True, "1 / 4"

```   
<br/><br/>  
  
### 3. 본인 컴퓨터에서 테스트하는 법
program.cs 파일의 main함수의 바로 처음에   
`BuildBot.BuildTestLab0.Test(Lab0.TryGetRepeatingDecimal, Lab0.TryGetIrreducibleFraction);`  
구문이 주석처리 되어있을 겁니다. 이 주석처리를 해제하고 빌드하시면 됩니다.   

빌드테스트를 전부 통과하면 요런 화면을 보실 수 있을겁니다.
![VsDebugConsole_sVDS8ElZUe](https://user-images.githubusercontent.com/70578707/131926102-7b322f5c-3774-4f9a-a246-432e335965fe.png)   

<br/>  <br/> 

실패한 테스트가 있다면 아래의 위키에서 확인하실 수 있습니다.   
https://docs.google.com/document/d/1Uuwt2idqyFusmnc6NSgeAqEm6cJ8rsWJ3oa0EZhmc6U/edit?usp=sharing

<br/><br/>
