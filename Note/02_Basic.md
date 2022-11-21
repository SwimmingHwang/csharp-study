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

- 자바와 유사

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

[Example 2 - 다차원배열]

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

- 가변 배열 (jagged array)
    - [m,n] 차원을 갖는 경우 무조건 m*n 개의 요소가 할당 돼 상황에 따라 자칫 메모리를 크게 낭비하는 경우가 발생한다. **하지만 가변 배열은 각 요소별로 필요한 만큼의 배열 크기를 임의로 결정할 수 있어 메모리를 최적화된 상태로 사용할 수 있다.**
        - 다만 기억하기 힘들고 유지보수가 m,n에 비해 쉽지 않기에 다차원 배열처럼 m*n개로 사용하는 경우가 좀 더 일반적이다

[Example 3 - 가변 배열(jagged array)]

```csharp
int[][] arr = new int[5][]; // 2차원 가변 배열

arr[0] = new int[10];
arr[1] = new int[9];
arr[2] = new int[8];
arr[3] = new int[3];
arr[4] = new int[5];
```

- `new` 키워드는 참조 형식과 함께 사용되는 경우 그에 필요한 메모리를 힙에 할당하는 역할을 함
- 배열의 값을 별도로 힙에 할당한다. **배열도 참조 형식에 속한다.**
- **자바와 달리 c# string에서는 개별 char 문자에 접근할 수 있는 대괄호 구문을 제공함**
    - string 타입이 인덱서를 구현햇기 때문에 배열처럼 다룰 수 있음
    - 반면에, java는 str.charAt(0) 이런식으로 메소드를 써야 했음

## 제어문

### 선택문

- 삼항 연산자(ternary operator) = 조건 연산자
    - 피연산자가 3개
    
    ```csharp
    int value = 5;
    string result = (value % 2 == 0) ? "짝수":"홀수"; // result에는 "홀수" 대입
    ```
    
- switch 문
    - switch (인스턴스)  인스턴스로 지정이 가능한 타입 : 정수형, 문자형, 불린형, 열거형(4절 객체지향 문법에 나옴)
    - 조건이 많아지면 swtich 문을 쓰는 편이 직관적인 코드 해석에 도움됨

```csharp
char ch = 'F';

switch (ch)
{
    case 'M':
        Console.WriteLine("남성");
        break;
    case 'F':
        Console.WriteLine("여성");
        break;

    default:
        Console.WriteLine("알 수 없음");
        break;
}
```

### 반복문

- 증감 연산자
    - foreach문
        - 배열, 컬렉션 사용 가능
    
    ```csharp
    int[] arr = new int[] { 1, 2, 3, 4, 5 };
    
    foreach (int elem in arr)
    {
        Console.WriteLine(elem);
    }
    ```
    

### 점프문

break, continue, goto, return, throw 

- break
- continue
    - 들여쓰기나 블록의 수를 줄일 수 잇어 **좀 더 구조적인 코드를 만들 수 있게 해줌**

```csharp
int sum = 0;
int n = 1;

while (n++ <= 1000)
{
    if ((n % 2) != 0) continue;
    if ((n % 3) != 0) continue;
    if ((n % 5) != 0) continue;
    sum += n;
}

Console.WriteLine(sum);
```

- goto
    - 제어문의 원조..
    - 가독성이 떨어짐
    
    ```csharp
    int sum = 0;
    int n = 0;
    
    LOOP:
    n++;
    
    if (n > 1000)
    {
        goto LOOPEXIT;
    }
    
    if ((n % 2) != 0) goto LOOP;
    sum += n;
    goto LOOP;
    
    LOOPEXIT:
    
    Console.WriteLine(sum);
    ```
    
    - gote는 절대 써서는 안 되는 것으로 단정 짓는 개발자들도 꽤 있지만,
    유용하다고 합의 보는 사례가 있음
    - **중첩 루프에서 탈출**
        - 전체 루프를 탈출하기 위해 별도의 조건 변수를 두고 이중으로 써야하는 구조가 나올 때 쓰면 이해하기 쉬운 구조로 바뀜
    
    ```csharp
    for (int x = 2; x < 10; x++)
    {
        for (int y = 1; y < 10; y++)
        {
            Console.WriteLine(x + " * " + y + " = " + (x * y));
            if (x == 5 && y == 8) goto LOOP_EXIT;
        }
    }
    
    LOOP_EXIT:;
    ```