[상위 문서로 이동](../README.md)

# OOP - Object Orineted Programming

최초의 컴퓨터 '애니악'부터 시작해서, C++이 출간되기 전까지 그간 많은 언어들이 존재하였었다. Assembly부터 시작해서 COBOL, Pascal 등등 현재도 가끔 쓰이는 언어들도 있었고, 지금도 많이 쓰는 **절차지향적 언어(Procedural Programming Language)** C언어도 또한 있었다. 다만 프로그램의 크기가 점점 커질수록, 절차지향적 언어만으로는 한계가 명확하게 드러나기 시작했다.

```c
typedef struct Animal {
  char name[30];  // 이름
  int age;        // 나이

  int health;  // 체력
  int food;    // 배부른 정도
  int clean;   // 깨끗한 정도
} Animal;
```

위 코드는 동물의 정보를 기록할 수 있는 구조체를 선언하였다. 그리고 하나의 변수를 생성하여 이를 필요로하는 함수들에게 변수 그대로를 전달해주었다.

```c
void play(Animal *animal);

Animal animal;
play(animal)
```

그런데 이렇게 코드를 작성하다보면 약간 헷갈리는 부분들이 있다. `Animal`이 `Play()`를 해야하는 것인데, 이렇게 되면 `Play`가 `Animal`을 하는 것이 아닐까? 라는 점이다. 솔직히 저 `Animal` 구조체에 `Play` 함수도 집어넣은 뒤 사용하면, 이미 구조체에 관련 변수들이 있으니 굳이 매개변수에 구조체 변수 인자를 넣어줄 필요도 없고 코드도 간결해질텐데 말이다.

이걸 해결해주는 것이 OOP, **객체지향 프로그래밍**이다. 

## 객체란?

> 변수들과 참고 자료들로 이루어진 소프트웨어 덩어리

객체를 생각하면 구조체에 메소드를 넣고 멤버 변수들을 설정해준 뒤, 실제로 동작하는 하나의 덩어리를 만들어 준다고 할 수 있다. 이 덩어리를 다르게 표현하면 **인스턴스**라고 하고 덩어리 안에 존재하는 변수와 메소드들을 각각 **인스턴스 변수**, **인스턴스 메소드**라고 할 수 있다. 

객체는 독립적으로 존재하고, 작동할 수 있다. 과정은 **클래스**를 통해 설계도를 짠 뒤, **인스턴스**를 생성하여 독립적인 객체를 만들어준다.

우리가 살고 있는 이 세상도 객체들이 가득한 세상에 살고 있다. 전자레인지로 예를 들자면, 작동 유무, 타이머, 소비전력 등이 인스턴스 변수가 될 것이고, 전자레인지 작동, 타이머 설정, 모드 설정 등이 인스턴스 메소드가 될 것이다. 이처럼 우리가 사용하고 있는 많은 것들을 전부 객체로 표현시킬 수 있다.

### 추상화(Abstraction)

> 불필요한 세부 사항들은 제거하고 가장 본질적이고 공통적인 부분만을 추출하여 표현하는 것

우리가 인스턴스를 생성할 때 무작정 같은 값들을 무수히 넣지만은 않는다. 똑같은 인스턴스 변수명이라도 각각 다른 값을 넣어주어 하나의 특징으로 잡아줄 수도 있는 것이다. 그런 근간을 잡아주는 것이 바로 추상화이다.

예를 들어, 자동차를 구현한다고 쳤을 때, 자동차는 정말 수많은 종류를 개발해낼 수 있다.(모닝이나 아반떼 등등..) 하지만 이 많은 종류의 자동차들도 공통적인 부분들을 가지고 있다. 이를테면 연료량이나 속도같은 변수들이나, 주행이나 정차같은 메소드들 말이다. 이런 공통적인 요소들을 묶어줄 수 있다.

### 캡슐화(Encapsulation)

> 외부에서 직접 인스턴스 변수의 값을 바꿀 수 없고 항상 인스턴스 메소드를 통해서 간접적으로 조절하는 것

보통 인스턴스의 값을 변경할 때, 외부에서 인스턴스 변수를 직접 건드리기 보다는 메서드를 이용해서 내부 변수들을 설정해준다. 그런데 왜 이런 번거로운 작업을 펼칠까?

대형 프로젝트로 넘어가게 될 경우에 보통 협업을 진행하는데, 다른 사람이 작성한 코드를 사용할 때 해당 코드를 이용하기 위해서 코드 전체를 이해하려고 하려면 머리가 터져버릴 것이다. 이를 단순화하기 위해서 존재하는데, 메서드를 통해서 특정 기능을 수행할 수 있다고만 명시를 해두면 굳이 코드 전체를 이해할 필요가 없기에 협업을 하는데 큰 도움이 되줄 것이다. 즉, *'내부 동작은 내가 알아서 할게. 넌 그냥 이 기능들을 사용하면서 응용만 해~'* 이런 느낌이다.

아니, 내부 동작이 정확히 어떻게 되는지도 모르는데 어떻게 코드를 잘 이용할 수 있겠냐? 라는 생각도 들 수 있다. 하지만 잘 생각해보자. 다시 자동차 예제로 넘어와서, 우리가 주행을 하는데 꼭 전체의 과정을 이해할 필요가 있겠는가? 액셀을 밟음으로써 기름이 엔진을 향해 흘러가고 엔진의 출력이 올라가면서 속도가 올라간다... 간단히 압축해도 이정돈데 이를 정확하게 이해하기 위해선 미분 같은 고급 수학과 엔진의 원리, 그리고 액셀레이터의 기름 조절량 등등 매우 고급적인 지식을 알아야 할 것이다. 하지만 우리가 주행을 하면서 그런걸 굳이 알 필요가 있는가? 아니다. 우리는 그냥 차를 주행함으로써 앞으로 나아가고, 목적지까지 이동하는 것이 자동차를 이용하는 주 목표이다. 마찬가지로 개발도, 필요한 경우에는 하나하나 다 개발해야겠지만 그렇지 않다면 그냥 메서드만 이용해서 다른 고급 기능들을 만들어가면 된다. 이 부분이 캡슐화의 큰 특징 중 하나이다.

실제로 엄청나게 거대한 프로그램 API(BPY 등등)를 살펴보면 긴 소스코드 대신 몇백개의 함수들과 메뉴얼들을 준다. 정리가 애매해서 하다가 좀 빡치긴 하지만 이 덕에 그 큰 프로그램을 무리없이 잘 사용할 수 있게 해준다.

## 클래스

이제 그 클래스에 대해 알아보자. 클래스는 C++에서(비단 다른 OOP 언어도 마찬가지로) **객체를 만들 수 있는 장치를 준비하는 설계도이다.**

예제 코드

```cpp
#include <iostream>

class Animal {
    private:
        int food;
        int weight;
    
    public:
        void set_animal(int _food, int _weight) {
            food = _food;
            weight = _weight;
        }
        void increase_food(int inc) {
            food += inc;
            weight += (inc/3);
        }
        void view_stat() {
            std::cout << "이 동물의 food    : " << food << std::endl;
            std::cout << "이 동물의 weight  : " << weight << std::endl;
        }
};

int main() {
    Animal animal;
    animal.set_animal(100, 50);
    animal.increase_food(30);

    animal.view_stat();
    return 0;
}
```

이렇듯 Class를 이용하면 Struct처럼 변수들도 지정해줄 수 있고, 내부 메서드들을 통해 내부 변수들을 제어해주면서 사용자는 속성 값만 전달해줄 수 있다. 클래스 내 변수, 메서드를 각각 **멤버 변수(Member Variable)와 멤버 함수(Member Function)**라고 부른다.

### 접근 제어 지시자

코드에 `public:`, `private:`가 있다. 이건 뭘까?

바로 외부에서 접근이 가능할 수 있는 부분들을 설정해주는 것이다. 예를 들어, 위에 서술했던 객체의 특징, *캡슐화*의 경우 메서드를 통해 변수들의 값을 설정해준다고 했었다. 이를 가능하게끔 하는 것이 바로 접근제어 지시자인데, 멤버 변수들을 `private`로 설정하여 외부 접근을 차단하고, 멤버 메서드들은 `public`으로 설정하여 외부에서 접근해 특정 기능들을 수행하도록 해줄 수 있다.

비단 캡슐화의 기능뿐만 아니라 보안적인 측면에서도 도움이 된다. 객체의 매우 중요한 역할들을 하는 몇몇 변수들과 메서드들을 외부에서 접근을 못하도록 막아줌으로써 데이터 유출 방지 및 변질을 보호하여 프로그램을 좀 더 안전하게 동작시켜줄 수 있다.

참고로 접근 제어 지시자를 설정하지 않은 변수와 메소드는 자동으로 `private:`로 설정된다.

## 단점

다만 OOP의 단점이 하나 있는데, 바로 **무겁다**라는 점이다. 변수들만 몇개 담는 구조체에 비해, 클래스는 변수는 기본이고 접근제어 지시자, 여러 속성들, 함수들까지 전부 내장하고 있기에 인스턴스를 찍어내릴수록 프로그램은 무거워질 수 밖에 없다. 이 점은 메인 메모리 용량 크기의 중요성을 부각시켜주기도 한다.

해서 OOP는 임베디드와 같은 적은 컴퓨팅 용량에는 적합하지 아니하고, 대형 응용 프로그램에 특화되어 있다.