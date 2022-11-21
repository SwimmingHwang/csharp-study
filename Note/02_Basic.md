# c# 기초

## 기본 자료형

- 정적 타입 언어이기 때문에 반드시 자료형 명시해야 함
- 실수형 기본 타입
    - float
        - 4바이트
        - 접미사 f
    - double
        - 8바이트
    - decimal
        - 16바이트
        - 반올림 오차가 허용되지 않는 회계 계산에 적합함
        - 소수점을 포함하는 경우 m을 붙여야 함
- 문자형 기본 타입
    - char
        - System.Char
        - 유니코드 16비트 문자
    - String
        - System.String
        - 유니코드 문자열
        - 큰따옴표

## 형변환

- 형변환
    - 암시적 변환
        - 범위가 작은 데이터 타입에서  큰 타입으로 형변환 가능 (컴파일 에러X)
    - 명시적 변환
        - 불가능 예시
        int n = 40000; // 큰 데이터 타입
        short s = (short) n;  // 작은 데이터 타입
        출력 결과 -25536
        - 가능한 예시 
        ushort u = 65;
        char c = (char) u;
        출력 결과 A

## 기본 문법 요소

- 변수
    - 저장소
        - 스택
            - 개별 스레드 마다 전용으로 사용할 수 있는 저장소가 메모리에 할당 됨. 그영역을 스택이라 함
            - 값 형식의 데이터를 저장함 
            int n = 5; 
            int : 4바이트 할당
            n : 저장소 이름
        - 힙
            - 프로그램에서 필요에 의해 메모리를 사용하겠다고 요청했을 때 사용할 수 있는 저장소
            - CLR이 직접 프로그램에서 사용될 힙 관리
            - 가비지 수집기에서 할당 및 해제 함
                - **참조 형식을 저장함**
    - `string text = “Hello”;`
        - string은 참조 형식 (refernce type)
        - text : 스택 저장소 이름
        - 스택 영역에 hello가 저장된 힙 영역의 주소(A번지)가 저장됨
        - 힙영역의 A번지에 Hello가 저장됨
    - `string text;`
        - text : 스택 저장소 이름
        - 초기화 되지 않은 모든 참조형 변수는 null 값을 가진다.
        - 스택 영역의 text가 가리키는 주소에 null 값이 들어가 있음

## 배열

- 자바와 동일   

[Example 1]

```csharp
int product1 = 5000;
int product2 = 5500;
int product3 = 6000;
int product4 = 10000;
int product5 = 60000;

int[] products = new int[5];
string[] names = new string[1000];

products[0] = 100;
products[1] = 200;
int book = products[0];
int sum = products[0] + products[1];

int[] products2 = new int[5] { 1, 2, 3, 4, 5 }; // 배열의 요소 개수를 지정
int[] products3 = new int[] { 1, 2, 3, 4, 5 }; // 배열의 요소 개수를 미지정

string text = "Hello World";
char ch1 = text[0];
char ch2 = text[1];

Console.WriteLine(ch1); // 출력 결과: H
Console.WriteLine(ch2); // 출력 결과: e
```

[Example 2]
```csharp
int[,] arr2 = new int[10, 5]; // 2차원 배열
short[,,] arr3 = new short[8, 3, 10]; // 3차원 배열

int[,] arr4 = new int[2, 3] 
{
    {1, 2, 3}, // 1차원의 요소 수는 3개이고,
    {4, 5, 6} // 2차원의 요소 수는 2개인 배열을 초기화
};

int[,,] arr5 = new int[2, 3, 4]
{
    {
        {1, 2, 3, 4}, // 1차원의 요소 수는 4개이고,
        {5, 6, 7, 8},
        {9, 10, 11, 12}, // 2차원의 요소 수는 3개이고,
    },

    {
        {13, 14, 15, 16},
        {17, 18, 19, 20},
        {21, 22, 23, 24},
    }, // 3차원의 요소 수는 2개인 배열을 초기화
};
```

[Example 3 - 가변 배열(jagged array)]
```csharp
int[][] arr = new int[5][]; // 2차원 가변 배열

arr[0] = new int[10];
arr[1] = new int[9];
arr[2] = new int[8];
arr[3] = new int[3];
arr[4] = new int[5];
```
