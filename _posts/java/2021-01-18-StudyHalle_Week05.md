---
layout: post
title: 스터디 할래 5. 클래스와 인스턴스
summary: 백기선님과 스터디 할래
author: devhtak
date: '2021-01-18 21:41:00 +0900'
category: Java Study
---

#### 목표
자바의 Class에 대해 학습하세요.

#### 학습할 것 (필수)
- 클래스 정의하는 방법
- 객체 만드는 방법 (new 키워드 이해하기)
- 메소드 정의하는 방법
- 생성자 정의하는 방법
- this 키워드 이해하기

- 용어 학습
  - 클래스: 객체(Object)를 만드는 틀
    - 필드: 클래스 내에서 정의한 객체의 속성/상태
    - 메서드: 클래스 내에서 정의한 객체의 행위
    - 생성자: 클래스로부터 만들어지는 인스턴스 변수를 초기화하기 위한 메서드
    - this: Class의 매개변수명과 Instance 변수명이 같을 경우 구별을 위해 사용하는 참조 변수

  - 인스턴스(Instance): Class로부터 만들어낸, 메모리 상(Heap)에 존재하는 실제 객체(Object)
    - new 키워드: 인스턴스를 만들 때 '생성자'를 호출하기 위해 사용하는 키워드

#### 클래스 정의하는 방법

- 객체의 상태와 행동이 정의된 하나의 클래스로 비슷한 구조를 갖되 상태는 서로 다른 여러 객체를 만들 수 있다.
- 필드(field) 
  - 필드는 해당 클래스 객체의 상태 속성을 나타내며, 멤버 변수라고도 불린다. 여기서 초기화하는 것을 필드 초기화 또는 명시적 초기화라고 한다.
  - 인스턴스 변수 
    - 이름에서 알 수 있듯이 인스턴스가 갖는 변수이다. 그렇기에 인스턴스를 생성할 때 만들어진다. 
    - 서로 독립적인 값을 갖으므로 heap 영역에 할당되고 gc에 의해 관리된다.
  - 클래스 변수
    - 정적을 의미하는 static키워드가 인스턴스 변수 앞에 붙으면 클래스 변수이다. 
    - 해당 클래스에서 파생된 모든 인스턴스는 이 변수를 공유한다. 
    - 그렇기 때문에 heap 영역이 아닌 static 영역에 할당되고 gc의 관리를 받지 않는다. 또한 public 키워드까지 앞에 붙이면 전역 변수라 볼 수 있다.

- 메서드(method)
  - 메서드는 해당 객체의 행동을 나타내며, 보통 필드의 값을 조정하는데 쓰인다.
  - 인스턴스 메서드
    - 인스턴스 변수와 연관된 작업을 하는 메서드이다. 인스턴스를 통해 호출할 수 있으므로 반드시 먼저 인스턴스를 생성해야 한다.
  - 클래스 메서드
    - 정적 메서드라고도 한다. 일반적으로 인스턴스와 관계없는 메서드를 클래스 메서드로 정의한다.
- 생성자(constructor) 
  - 생성자는 객체가 생성된 직후에 클래스의 객체를 초기화하는 데 사용되는 코드 블록이다. 메서드와 달리 리턴 타입이 없으며, 클래스엔 최소 한 개 이상의 생성자가 존재한다.
- 초기화 블록(initializer) 
  - 초기화 블록 내에서는 조건문, 반복문 등을 사용해 명시적 초기화에선 불가능한 초기화를 수행할 수 있다.
  - 클래스 초기화 블록
    - 클래스 변수 초기화에 쓰인다.
  - 인스턴스 초기화 블록
    - 인스턴스 변수 초기화에 쓰인다.
    
  ```
  클래스 변수 초기화: 기본값 → 명시적 초기화 → 클래스 초기화 블록
  인스턴스 변수 초기화: 기본값 → 명시적 초기화 → 인스턴스 초기화 블록 → 생성자
  ```

- 접근 제어자 
  - 접근 제어자는 해당 클래스 또는 멤버를 정해진 범위에서만 접근할 수 있도록 통제하는 역할을 한다. 
  - 클래스는 public과 default밖에 쓸 수 없다. 범위는 다음과 같다. 참고로 default는 아무것도 덧붙이지 않았을 때를 의미한다.
  
    |접근제어자|동일 클래스|동일 패키지|자손 클래스|그 외 영역|
    |---|---|---|---|---|
    |public|O|O|O|O|
    |protected|O|O|O|-|
    |default|O|O|-|-|
    |private|O|-|-|-|
    
- static
  - 변수, 메서드는 객체가 아닌 클래스에 속한다.
- final
  - 클래스 앞에 붙으면 해당 클래스는 상속될 수 없다.
  - 변수 또는 메서드 앞에 붙으면 수정되거나 오버라이딩 될 수 없다.
- abstract
  - 클래스 앞에 붙으면 추상 클래스가 되어 객체 생성이 불가하고, 접근을 위해선 상속받아야 한다.
  - 변수 앞에 지정할 수 없다. 
    - 메서드 앞에 붙는 경우는 오직 추상 클래스 내에서의 메서드밖에 없으며 해당 메서드는 선언부만 존재하고 구현부는 상속한 클래스 내 메서드에 의해 구현되어야 한다.
- transient 
  - 변수 또는 메서드가 포함된 객체를 직렬화할 때 해당 내용은 무시된다.
- synchronized 
  - 메서드는 한 번에 하나의 쓰레드에 의해서만 접근 가능하다.
- volatile
  - 해당 변수의 조작에 CPU 캐시가 쓰이지 않고 항상 메인 메모리로부터 읽힌다.

#### 객체 만드는 방법 (new 키워드 이해하기)

- 클래스에서 객체를 생성하려면 아래와 같이 new키워드를 생성자 중 하나와 함께 사용하면 된다.
- new키워드
  - 새 객체에 메모리를 할당하고 해당 메모리에 대한 참조값을 반환하여 클래스를 인스턴스화한다.
  - 일반적으로 객체가 메모리에 할당되면 인스턴스라 부른다.

#### 메소드 정의하는 방법

```java
public void setter(int variable) {
// 접근제어자 / 반환 타입 / 메서드 이름 / (매개변수 리스트) / -> 선어부
    this.variable = variable; // 구현부
}
```
- 접근 제어자 및 기타 제어자 
  - 해당 메서드에 접근할 수 있는 범위를 명시하거나 부가적인 의미를 부여한다.
- 반환 타입
  - 메서드가 모든 작업을 수행한 뒤에 반환할 타입을 명시한다.
- 메서드 이름 
  - 메서드명은 동사여야 하고 lowerCamelCase를 따르며 뜻이 명확해야 한다. 
  - 메서드를 호출할 때 사용한다 (+ 매개변수도 주어야 한다)
- 매개변수 리스트
  - 메서드에서 사용할 매개변수들을 명시한다.
- 메서드 시그니처
  - 컴파일러는 메서드 시그니처를 보고 오버로딩(overloading)을 구별한다. 물론 리스트의 순서도 동일해야 한다.

#### 생성자 정의하는 방법

- 생성자를 명시하지 않으면 컴파일러가 자동으로 기본 생성자를 생성한다. (바이트 코드로도 확인 가능)
- 하지만 기본 생성자가 아닌 다른 형태의 생성자만 명시했다면 기본 생성자는 컴파일시에 생성되지 않는다.

#### this 키워드 이해하기

- this키워드는 인스턴스 자신을 가르킨다. 
- 클래스 메서드에서는 this를 쓸 수 없다. 인스턴스가 생성되지 않은 상태에서 사용되기 때문이다.
- this() 는 매개변수가 없는 생성자를 호출한다. 생성자 체이닝에서 사용할 수 있다.