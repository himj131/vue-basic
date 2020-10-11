# 뷰 템플릿
#### 뷰 템플릿이란?
- HTML,CSS등의 마크업 속성과, 뷰 인스턴스에서 정의한 테이터와 로직을 연결해 HTML로 변환해 주는 속성
- template속성에서 정의한 마크업+뷰데이터는 가상돔 기반의 render()함수로 변환되고, 변환된 render함수는
최종적으로 사용자가 볼수 있는 화면을 그린다. 이 변환 과정에서 뷰 반응성(Reactivity)이 더해진다.

## 템플릿에서 사용하는 뷰의 속성과 문법
#### 데이터 바인딩
- 데이터바인딩(data-binding)은 HTML화면 요소를 뷰 인스턴스의 데이터와 연결하는 것을 의미한다.
- {{}}문법과 v-bind속성을 사용한다.
    - 콧수염 괄호({{}})
       - 뷰 인스턴스의 데이터를 HTML 대그에 연결하는 기본적인 텍스트 삽입방식
        ``` js
        <div id = "app">
            //data 속성의 message값이 바뀌면 뷰 반응성에 의해 화면이 자동으로 갱신됨
            {{message }} 
        </div>
        
        <script>
            new Vue({
                el: '#app';
                data: {
                    message: 'Hello Vue.js!'
                }
            });
        </script>
        ```
      - 뷰 데이터가 변경되어도 값을 바꾸고 싶지 않다면 `v-once`속성을 사용한다.
      ``` js
        <div id = "app" v-once>
            {{message }} 
        </div>
        ...
      ```
    - v-bind
        - 아이디, 클래스, 스타일 등의 HTML 속성(attributes)값에 뷰 데이터 값을 연결할 때 사용하는 데이텨 연결 방식
        - `v-bind:` 문법은 `:`로 간소화 할 수 있다. 따라서 v-bind:id 와 :id는 같은 동작을 한다.  
        - 뷰 코드가 전반적으로 v-접두사를 사용하기 때문에 가급적 v-bind속성을 이용하는 것이 기존 HTML문법과 구분도 되고 다른사람이 파악하기도 쉽다.
        ``` 
            /* 
            HTML기본 속성인 id, class, style의 앞에 v-bind:를 붙여서
            뷰 인스턴스에 정의한 데이터 속성과 연결하여 화면에 나타내기
            */
            <div id = "app">
                <p v-bind:id="idA">아이디 바인딩</p>
                <p v-bind:class="classB">클래스 바인딩</p>
                <p v-bind:style="styleC">스타일 바인딩</p>
            </div>
            <script>
                new Vue({
                    el: '#app';
                    data: {
                        idA: 10,
                        classB: 'container',
                        styleC: 'color:blue'
                    }
                });
            </script>
        ```
        
#### 자바스크립트 표현식
#### 디렉티브
#### 이벤트 처리
#### 고급 템플릿 기


