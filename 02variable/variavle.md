## 변수

### 변수선언
- `var` 과 비슷하게 `let` 을 이용하여 변수를 선언한다

```JavaScript
let title = '제목';
console.log(title);

title = '제목수정';
console.log(title);
```

- 변수명은 `Identifier` 하게 선언하여야 한다.
- `let`을 이용하여 선언시 중복되는 변수명은 에러를 발생

```JavaScript
let title = '제목';
let title = '제목수정'; // SyntaxError
console.log(title);
```

- `let` 을 이용하여 선언한 변수는 `local` 하게만 사용 가능하다.

```JavaScript
let globalScope = 'global name';
    {
        let name = 'javascript';
        console.log(name);
        name = 'hello';
        console.log(name);
    }
console.log(name); // 아무것도 출력하지 않는다 scope가 다르다
console.log(globalScope);
```

- `var`을 이용하여 선언한 변수는 `global`하게 참조될 수 있다.
- **가장 가까운 스코프에서 초기화된 변수로 할당된다!**

```JavaScript
let globalScope = 'global name';
{
    var name = 'javascript';
    console.log(name); // javascript
    name = 'hello';
    console.log(name); // hello
}
console.log(name); // hello 
console.log(globalScope) // global name
```
