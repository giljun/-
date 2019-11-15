# Vue

## 사전지식

### Virtual DOM이란 무엇인가?

- Vue.js 2.0에서부터도 사용

- Virtual DOM 기술은 DOM 조작에 있어 비효율적인 이유에서 나오게 되었다.

  - DOM 조작이 비효율적인 이유

    - 기존에는 아래와 같이, Javascript 또는 Jquery를 통해 원하는 dom 노드를 찾은 후 변경하는 행위를 했다.

      ```javascript
      document.getElementById('myid').appendChild(myNewNode) // javascript
      $('#myid').append(myNewNode) // jquery
      ```

    - 수천 가지의 노드가 존재할 수 있기에, 계산하기 위해 큰 비용을 투자하게 된다.

    - 성능 저하로 인한 페이지 속도 지연이 발생한다.

    - 아래의 그림과 같은 동작이 DOM 조작을 할 때마다 영향을 끼치게 되는 것이다.

  - Virtual DOM Code

    ```javascript
    let domNode = {
        tag: 'ul'
        attributes: { id: 'myid' }
    	children: [
            // where the LI's would go
        ]
    };
    ```

    - domNode 객체를 Virtual DOM으로 보면 된다.
    - 직접 DOM API를 사용하지 않고, domNode 객체를 활용하게 된다.
    - 실제 DOM이 아닌 메모리에 있기 때문에 훨씬 더 빠르다.
    - 변경된 부분만 찾아 실제 DOM에 변경해주는 방식이다.



## 장점

### 학습 곡선이 낮다.

- 사람마다 다를 순 있으나, 알려진 학습 곡선은 Angular > React > Vue 순



### 컴포넌트

- 대규모 프로젝트에 있어, 유지보수와 재사용성을 높이기 위해 작은 단위로 쪼개서 관리한다.
- 현재 개발 구조로 이미 컴포넌트 방식이 대세이며, 추세이다.
- 단일 파일 컴포넌트
  - .vue 파일 하나에 html, css, js를 작성할 수 있다.
  - 캡슐화를 제공



### 성능

- 가볍고 빠르다
- 적은 오버헤드와 빠른 성능
- Virtual DOM에 있어서도, React와 비교해서 보다 효과적인 성능을 낸다고 알려져있다.



### View 최적화

- MVVM 패턴에 영감을 받아서, View에 최적화되어있다.
- DOM 조작에 있어, 기존 jQuery를 통한 DOM 조작은 더이상 필요하지 않다.
- View의 동적 변화에 대한 처리가 매끄럽고 용이하다.



### 많은 모듈

- 중앙 집중식 상태 관리 저장소를 위한 vuex
- SPA를 위한 vue-router
- 유효성 검증을 위한 vue-validator
- HTTP, Ajax를 위한 vue-resource
- Vue에 최적화된 개발자 모드를 위한 vue-devtools 등등
- 효율적이고, 필요한 모듈이 웬만하면 존재하고, 이것 또한 학습곡선이 높지 않다.