# Algorithm



- **배열 초기화**

```java
int[] arr1 = new int[1];
int[] arr2 = new int[]{1,2,3};  //저장할 요소만 지정
int[] arr3 = {1,2,3,4,5};   
```



- **toString()**

   배열의 요소들을 문자열로 조합하여 반환



- **foreach : 향상된 for문**

  - 더욱 직관적, 오류 가능성 낮춤.
  - 첨자 변자 대신 배열의 요소를 저장할 변수를 선언하고, : 과 함께 순회할 배열의 참조 변수를 선언
  - 배열의 연산으로 특정 위치에 값을 삽입, 삭제하거나 값을 읽어오는 경우, 사용 불가
    ex) for(int nums : students)  ...
    
    

- **Random**

  - nextInt(ARRAY_LENGTH) - 난수 생성
    - ARRAY_LENGTH는 난수의 범위를 지정. 만약 100이면 0~99까지의 난수



```java
import java.util.Random; 

//N번만큼 반복하며 소수만 배열에 저장 
//소수는 1 또는 자기 자신으로만 나누어지는 값. 
//2부터 자신의 -1까지 나누어 한번이라도 0으로 떨어진다면 소수가 아님! 
public class randomEx_2 { 
    public static void main(String args[]) {
        Random ra = new Random(); //랜덤 객체 생성 
        final int ARRAY_LENGTH = 100; //길이를 10으로 지정 
        int[] arr = new int[ARRAY_LENGTH]; //길이가 ARRAY_LENFTH인 배열 생성
        
        for(int i=0; i<ARRAY_LENGTH; i++) { 
            boolean isPrimeNumber = true; 
            int randomValue = ra.nextInt(100); //난수 생성, nextInt 안에 있는 값은 난수의 범위를 지정. 
            
            if(randomValue == 1) { 
                continue; 
            } 
            if(randomValue == 2) { 
                arr[i] = randomValue; 
                continue; 
            } 
            
            for(int j =2; j<randomValue; j++) {  //소수구하기
                if(randomValue % j == 0) {  //나눠 떨어지면 소수가 아님
                    isPrimeNumber =  false; 
                    break; 
                } 
            } 

            if(isPrimeNumber) { 
                arr[i] = randomValue; 
            } 
        } 
        
        System.out.print("소수: "); 
       
        for(int k : arr) { 
            if(k>0) { 
                System.out.print(k+" "); 
            } 
        } 
    } 
}
```


- **배열 복사 메서드**

  1. clone()

  2. System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
      - 5개의 인자(parameter)
          - 원본 배열 객체, 원본 배열에서 복사할 시작점, 사본 배열 객체, 사본 배열에서 복사할 시작점, 원본 배열의 요소를 복사할 개수

  3. Arrays.copyOf(...)
       - 2개의 인수(argument)
          - 복사할 객체, 복사할 크기

  4. Arrays.copyRange(...)
       - 3개의 인수
           - 복사할 객체, 복사할 시작점, 복사할 끝 점



- **다중 배열**

  - 2차원 배열 구구단

```java
//구구단 
public class multiEx { 
    public static void main(String args[]) { 
        int[][] arr = new int[8][9];  //행 8, 열 9인 이차원 배열 생성
 
        for(int i=0, k=2; i<arr.length; i++, k++) {  //8이 되기 전까지  
            for(int j=0; j<9; j++) { 
                arr[i][j] = k * (j+1); //값 계산 
            } 
        } 
        
        for(int i=0; i<arr.length; i++) { 
            for(int j=0; j<9; j++) { 
                if(j!=0 && j%3==0) { 
                    System.out.println("");  //한줄 넘기기 
                } 
                System.out.print((i+2)+"x"+(j+1)+"="+arr[i][j]); 
                System.out.print(" "); 
            } 
            System.out.println("\n"); 
        } 
    } 
}
```



