

# Chapter02 : DOM추상화의 내부

## 주요내용

### JSX

> 자바스크립트 코드 안에 선언적인 XML 스타일의 구문을 작성할 수 있게 해주는 리액트의 선택적 자바스크립트 구문 확장

- 작동 원리

  - JSX로 작성된 XML 스타일 구문이 JS 코드로 변환됨 ([createElement](https://github.com/facebook/react/blob/v15.0.0-rc.1/src/isomorphic/classic/element/ReactElement.js#L117))

    ```
    <Nav color="blue" />
    ```

    ```
    React.createElement(Nav, {color: 'blue'})
    ```

- HTML과의 차이점

  - 태그 특성은 낙타 표기법으로 작성.

  - 모든 요소는 짝이 맞아야 함. 

  - 특성 이름이 HTML 언어 사양이 아닌 DOM API에 기반을 둔다.

    - HTML

      ```
      <div id="box" class="some-class"></div>
      ```

    - 자바스크립트로 DOM 조작 

      ```
      document.getEIementByld("box").className="some-other-class"
      ```

    - JSX

      ```
      return <div id="box" className="some-class"></div>
      ```

- JSX 특징  

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

    - JSX 내에서 주석을 작성할 때는 { /* comments */ } 사용 (HTML 주석이 아닌 자바스크립트 주석)

- JSX 를 사용하지 않는다면?

  - 일반 자바스크립트로 React Component 구성

    ```
    let child1 = React.createElement('li', null, 'First Input');
    let child2 = React.createElement('li', null, 'Second Input');
    let root = React.createElement('ul', {className:'inputList'}, child1, child2);
    React.render(root,document.getElementById('root'));
    ```

  - 일반적인 HTML 태그 사용할 수 있도록 React.DOM에서 함수 제공

    ```
    React.DOM.form({className:'testForm'},
        React.DOM.input({type:"text", placeholder:"Name"}),
        React.DOM.input({type:"text", placeholder:"ID"}),
        React.DOM.input({type:"submint", value:"Post"})
    )
    ```

### 가상 DOM

> 어플리케이션의 상태가 바뀔 때마다, 실제 DOM을 다시 생성하지 않고 비슷한 가상트리를 생성해서 효육적으로 업데이트!

- 작동방식

  - DOM을 가상 메모리에 하나 더 만들어 유지 (돔을 직접 건드리기 보다 추상화된 버전을 만듬)
  - render() 함수는 실질적으로 가상DOM을 반환.
  - 메모리상에 있는 가상DOM을 실제 DOM과 가장 빠른 방식으로 비교하여 브라우저 내용을 업데이트! (알고리즘 적용)
  - 효율적으로 서브 트리만 업데이트 하는 것 => react에서는 heuristic algorithm을 사용.

- Key (키) / Ref (실제 DOM 접근)

  - 브라우저와 상호작용 하기 위하여 DOM node에 대한 reference가 필요함. 
  - key 지정을 항상 제대로 해주어야 가능.

  ​

## 궁금한 사항

- Ref를 사용한 사례가 뭐가 될가? 크게 와닿지가 않는다 책만봐서는.
- ​

## 참고자료

- http://www.lispcast.com/what-is-react


- http://blog.sapzil.org/2016/03/17/react-internals-elements/


- http://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/ (번역: http://blog.sejongin.kr/51)
- http://johnohblog.com/react-virtual-dom-2/
