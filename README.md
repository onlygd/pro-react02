

# Chapter02 : DOM추상화의 내부

## 주요내용

### JSX

> 자바스크립트 코드 안에 선언적인 XML 스타일의 구문을 작성할 수 있게 해주는 리액트의 선택적 자바스크립트 구문 확장

- HTML과의 차이점

  - 태그 특성은 낙타 표기법으로 작성.

  - 모든 요소는 짝이 맞아야 함. 

  - 특성 이름이 HTML 언어 사양이 아닌 DOM API에 기반을 둔다.

    ```
    HTML : <divid="box''clas5="some-class"></div>
    ```

    ```
    자바스크립트로 DOM 조작 : document.getEIementByld(''box'').ClassName="some-other-cla5s"
    ```

    ```
    JSX : return <div id="box''Cla5sName="some-class"></div>
    ```

- JSX 특이점  

  - Nested Element (단일 루트 노드)

    ```
     return  (
                <h1> Hello Velopert</h1>
                <h2> Welcome </h2>
     );
    ```

    ```
    ERROR in ./src/App.js
    Module build failed: SyntaxError: /home/vlpt/node_tutorial/react/react-tutorials/03-jsx/src/App.js: Adjacent JSX elements must be wrapped in an enclosing tag (10:12)
       8 |         return  (
       9 |             <h1> Hello Velopert</h1>
    > 10 |             <h2> Welcome </h2>
         |             ^
      11 |         );
      12 |     }
      13 | }
    ```

    다음과 같은 경우 오류 발생. 루트객체 하나에 래핑해야 함 (꼭, Container element안에 포함시켜야 함)

    ```
    return  (
                <div> {/* Container */}
                    <h1> Hello Velopert </h1>
                    <h2> Welcome </h2>
                </div>
    );
    ```

  - JavaScript Expression

    - { } 로 wrapping해서 사용
    - 조건절 (If-Else 사용 불가) -> 삼항식(condition ? true : false)을 이용하거나, 별도 스크립트로 빼서 사용

  - Inline Style

    - string 형식이 아닌, key가 camelCase 인 Object를 적용

  - Comments

    - JSX 내에서 주석을 작성할 때는 { /* comments */ } 사용

 

### 가상 DOM

> 어플리케이션의 상태가 바뀔 때마다, 실제 DOM을 다시 생성하지 않고 비슷한 가상트리를 생성

- 작동방식

  - DOM을 가상 메모리에 하나 더 만들어 유지
  - render() 함수는 실질적으로 가상DOM을 반환
  - 메모리상에 있는 가상DOM을 실제 DOM과 가장 빠른 방식으로 비교하여 브라우저 내용을 업데이트! (알고리즘 적용)

- Key (키)

  ```
  Before : <1i>Orange</li><li>Banana(/1i>
  ```

  ```
  After  : <li>Apple</li><1i>Orange</1i>
  ```

  - DOM Tree간에 항목 삭제,삭제,대채 등 여부를 파악하기 위해, 빠르게 조회할 수 있게 하는 고유 식별자

- Ref 

  - 실제 DOM에 접근
  - ​



## 궁금한 점







## 참고자료

http://www.lispcast.com/what-is-react
