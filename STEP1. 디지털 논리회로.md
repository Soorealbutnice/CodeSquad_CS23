### STEP1. 디지털 논리회로

---

> #### NAND 게이트

- NAN게이트 출력

|   NAND    | false | true  |
| :-------: | :---: | :---: |
| **false** | true  | true  |
| **true**  | true  | false |

- NAND 게이트 동작을 함수로 구현한다.
- 함수의 매개변수는 BOOL 타입을 갖는 두 개를 갖고, 결과값은 BOOL 타입으로 리턴합니다.
- paramA 와 paramB 가 모두 true 일 때만 결과가 false 가 되고, 나머지 다른 경우는 모두 true가 됩니다.
- 

```java
public boolean nand(boolean paramA, boolean paramB) {
    boolean answer = true;
    
    if ( paramA == true && paramB == true) {
        answer = false;
    }
    
    return answer;
}

// 다른 풀이
public boolean nand(boolean paramA, boolean paramB) {
    boolean answer = true;
	
    answer = !(paramA && paramB);
    	
    return answer;
}

```



> #### NOR 게이트

- NOR 게이트 출력

| NOR       | false | true  |
| --------- | ----- | ----- |
| **false** | true  | false |
| **true**  | false | false |

- NOR게이트 동작을 구현합니다.
- 함수의 매개변수는 BOOL 타입을 갖는 두 개를 갖고, 결과값은 BOOL 타입으로 리턴합니다.
- paramA 와 paramB 가 모두 false 일 때만 결과가 true 가 되고, 나머지 다른 경우는 모두 false가 됩니다.

```java
public boolean nor(boolean paramA, boolean paramB) {
    boolean answer = true;
    
    if ( paramA != false && paramB != false) {
        answer = false;
    }
    
    return answer;
}

// 다른 풀이
public boolean nor(boolean paramA, boolean paramB) {
   
    boolean answer = !(paramA || paramB);   
  
    return answer;
}
```



> #### 이진 덧셈기

##### 미션1

```java
import java.util.Arrays;

class Adder {
    // 반가산기
    public int[] halfadder(int bitA, int bitB) {
    	int[] answer = new int[2];
    	
        if (bitA == 1 && bitB == 1) {
        	answer[0] = 1;
        	answer[1] = 0;
        } else if (bitA == 0 && bitB == 0) {
        	answer[0] = 0;
        	answer[1] = 0;
        } else {
        	answer[0] = 0;
        	answer[1] = 1;
        }
        
        System.out.println(Arrays.toString(answer));
        return answer;
    }
    
    // 전가산기
    public int[] fulladder(int bitA, int bitB, int carry) {
    	int[] answer = new int[2];
    	
    	int total = bitA + bitB + carry;
    	
    	if (total == 3) {
    		answer[0] = 1;
    		answer[1] = 1;
    	} else if (total == 2) {
    		answer[0] = 1;
    		answer[1] = 0;
    	} else if (total == 1) {
    		answer[0] = 0;
    		answer[1] = 1;
    	} else {
    		answer[0] = 0;
    		answer[1] = 0;
    	}
    	
    	System.out.println(Arrays.toString(answer));
        return answer;
    }
    
    public static void main(String[] args) {
    	Adder adder = new Adder();
    	adder.halfadder(1, 1);
    	adder.fulladder(1, 1, 1);
	}
}
```



##### 미션1 다시 풀기

```java
class Adder {
    public boolean[] halfadder(boolean bitA, boolean bitB) {
        boolean[] answer = new boolean[2];
        
        // carry    
        answer[0] = biteA && biteB;
        
        // sum
        answer[1] = !biteA && biteB || biteA && !biteB;
        
        return answer;
    }
    public boolean[] fulladder(boolean bitA, boolean bitB, boolean carry) {
        boolean[] answer = new boolean[2];
        
        // C
        answer[0] = biteA && biteB || biteA && carry || biteB && carry;
        
        // S
        answer[1] = !biteA && !biteB && carry || !biteA && biteB && !carry ||
            		biteA && !biteB && !carry || biteA && biteB && carry;
        
        return answer;
    }
}
```



> #### 진법 변환기

##### 미션1

0부터 256 미만의 `Int` 정수형 10진수를 `[Bool]` 2진수 배열로 변환하는 dex2bin 함수를 구현한다.

```java
import java.util.ArrayList;

class Convertor {
	
    public static ArrayList<Integer> dec2bin(int decimal) {
        ArrayList<Integer> answer = new ArrayList<Integer>();
        
        while (decimal / 2 != 0) {
            answer.add(decimal % 2);
            decimal = decimal / 2;
	    }
        answer.add(1);
        
        return answer;
    }
	
	public static void main(String[] args) {
		
		int decimal = 173;
		
		ArrayList<Integer> arr = dec2bin(decimal);
		
		for (int i = 0; i < arr.size(); i++) {
			System.out.println(arr.get(i));
		}
	        
	}
}
```



##### 미션2

`[Bool]` 2진수 배열을 `Int` 정수형 10진수로 변환하는 bin2dec 함수를 구현한다.

```java
public class Bin2deci {
    public int bin2dec(int[] bin) {
        int answer = 0;
        
        for (int i = 0; i < bin.length; i++) {
        	answer += bin[i] * Math.pow(2, i);
        }
        
        return answer;
        
    }
}
```

