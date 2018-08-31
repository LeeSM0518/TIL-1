# Classes

[![npm](https://img.shields.io/badge/version-2018.35-brightgreen.svg)]()

## Introduction





## Classes

간단한 클래스 기반 예제를 살펴 보겠습니다.

~~~typescript
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
~~~

만약 C#이나 Java를 이전에 사용해봤다면, 구문들이 익숙할 것입니다. 위의 예제에서 ```Greeter``` 클래스를 선언하였습니다. 이 클래스는 3개의 멤버(member)를 가지고 있으며 각각 프로퍼티(property)라 불리는 ```greeting```, 생성자(constructor) 그리고 메서드(method)인 ```greet```입니다. 

또한 클래스 내부에서 클래스가 가지는 멤버를 가리킬 때 ```this.```를 사용한다는 것을 알 수 있습니다.  

마지막 라인에서 우리는 ```new``` 를 사용하여 `Greeter` 객체를 생성하였습니다.  이 동작은 미리 정의한 생성자를 호출하여  `Greeter` 의 객체를 생성하고 초기화합니다.



## Inheritance



## Public, private, and Protected modifiers



## Readonly modifier



## Accessors

타입스크립트는 객체의 멤버에 접근할 수 있는 방법으로서 getter와 setter를 지원합니다. 이렇게하면 각 객체에서 멤버가 액세스되는 방식을 세밀하게 제어 할 수 있습니다.

간단한 클래스를 `get` 과 `set`을 사용하도록 변환해봅시다. getter와 setter가 없는 클래스부터 살펴봅니다.

```typescript
class Employee {
    fullName: string;
}

let employee = new Employee();

employee.fullName = "Bob Smith";

if (employee.fullName) {
    console.log(employee.fullName);
}
```

손쉽게 `fullname`을 수정할 수 있지만 `fullname`이 자주 변경되는 경우 문제를 발생시킬 수 있습니다. 

아래와 같이 수정된 코드에서는 employee에 대해 수정하기 전에 사용자가 올바른 passcode를 가지고 있는지 확인 할 수 있습니다. `fullname`에 직접적으로 접근하는 것 대신 `set`을 이용하여 passcode를 체크할 수 있습니다. 또한 getter도 추가하였습니다.

```typescript
let passcode = "secret passcode";

class Employee {
    private _fullName: string;

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        if (passcode && passcode == "secret passcode") {
            this._fullName = newName;
        }
        else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    console.log(employee.fullName);
}
```

접근자(accessor)가 passcode를 확인하고 있음을 증명하기 위해 passcode를 수정하고 일치하지 않을 때 직원에게 업데이트 할 수있는 권한이 없다는 경고 메시지를 보낸다는 것을 확인합니다.

접근자에 대해 알아야할 점이 두 가지 있습니다.

첫째로 접근자는 ECMAScript 5 이상의 자바스크립트 코드가 나올 수 있도록 컴파일러를 설정해야합니다. ECMAScript 3 하위 레벨은 지원되지 않습니다. 둘째로(이건 나중에 다시보고 이해)





 



## Static Properties



## Abstract Classes



## Advanced Techiques


