# vtable

가상 테이블(vtable)은 c++에서 **다형성을 지원하기 위해 생성되는 특별한 데이터 구조이다.**

클래스가 가상 함수를 포함할 때 컴파일러가 자동으로 생성해준다.

객체가 가상 함수를 호출할 때, 컴파일러는 이 가상 테이블을 참조하여 올바른 함수를 런타임에 호출한다.

**가상 테이블의 구조와 역할**

1. **가상 테이블(vtable)**: 클래스마다 하나씩 생성되고, 해당 클래스에서 사용할 수 있는 가상 함수들의 **포인터 목록**을 포함한다. 이를 통해 가상 함수 호출이 가능하다.

2. **가상 테이블 포인터(vptr)** : 클래스가 인스턴스화되면, **각 개체마다 vptr이 설정**된다. vptr은 해당 객체의 가상 테이블을 가리키고, 이를 통해 객체가 실제로 가리키는 클래스의 가상 테이블을 찾아간다.

**가상 함수 호출 과정**

1. **vptr을 통해 vtable 접근**: 컴파일러는 객체의 vptr을 통해 가상 테이블을 참조한다.

2. **vtable에서 올바른 함수 찾기**: 가상 테이블에서 해당 가상 함수에 대한 포인터를 찾아가서 이 포인터가 가리키는 함수로 이동한다.

3. **함수 호출**: 최종적으로 가리킨 함수를 호출하여 다형성 기능을 구현하게 된다.

		#include <iostream>

		class B {
		public:
			B() { std::cout << "B 생성자" << std::endl;};
			virtual ~B() {std::cout << "B 소멸자" << std::endl;};
		};
		
		class A : public B{
		public:
			A() { std::cout << "A 생성자" << std::endl;};
			~A() {std::cout << "A 소멸자" << std::endl;};
		};
		
		int main() {
			B *b = new A();
		 // 이 경우에 b의 vptr은 A의 vtable을 가르킨다.
		    return 0;
		}
