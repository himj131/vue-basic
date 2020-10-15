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
- {{}} 안에 자바스크립트 표현식을 넣어 자바스크립트 표현식을 사용할 수 있다. ([예제코드 바로가](../5template/useJavaScript.html))
- 자바스크립트의 <u>선언문과 분기 구분은 사용할 수 없다.</u> (삼항 연산자는 가능)
- 연산은 HTML단에서 수행하는것 보다는,   
자바스크립트 단에서 `computed`속성을 이용하여 계산하고 최종값만 표시하는것을 권장 ([예제코드 바로가](../5template/computed.html))
    > HTML에 최종적으로 표현될 값만 나타내고, 데이터의 기본 연산은 자바스크립트에서 함으로써   
      화면단 코드 가독성을 높여 UI구조를 쉽게 파악할 수 있다.
- computed를 사용하면 반복적인 연산에 대해서는 미리 계산하여 저장해 놓고 필요할 때 바로 불러오는 캐싱(caching)효과를 얻을 수 있다.

#### 디렉티브기
- 뷰 디렉티브(Directive)란 HTML 태그 안에 v- 접두사를 가지는 모든 속성들을 의미한다.
- `<a v-if="flag">링크</a> 형식을 가진다.
- 디렉티브를 활용하 데이터 값이 변경되었을 때, 화면 요소들이 리액티브하게 반응하여 변경된 데이터 값에 따라 갱신되도록 한다.(직접제어 필요x)
- 자주 사용하는 주요 디렉티브
    - v-if : 지정한 뷰 데이터 값의 참, 거짓 여부에 따라 HTML태그를 화면에 표시하거나 표시하지 않음.
    - v-for : 지정한 뷰 데이터의 개수만큼 해당 HTML 태그를 반복 출력
    - v-show : v-if와 유사하게 데이터 진위여부에 따라 해당 HTML태그를 화면에 표시하거나 표시하지 않는다.
- [디렉티브 동작코드 보기](../5template/directive.html)  
> v-if와 v-show 의 차이  
> v-if는 태그를 완전히 삭제하지만, v-show는 css효과만 display:none; 으로 주어 실제 태그는 남아 있고 화면상으로만 보이지 않는다.
#### 이벤트 처리
- 이벤트 처리를 위해 뷰에서는 v-on디렉티브와 methods 속성을 활용한다.
    - 클릭 이벤트
        ```js
          ...
          <button v-on:click="clickBtn">클릭</button>
          ...
          <script>
            methods: {
              clickBtn: function() {
                  alert('clicked');
              }   
            }     
          </script>
        ```
  
    - 클릭 이벤트(메서드 호출시 인자값 넘기기)
        ```js
          ...
          <button v-on:click="clickBtn">클릭</button>
          ...
          <script>
            methods: {
              clickBtn: function() {
                  alert('clicked');
              }   
            }     
          </script>
        ```
    - v-on:click 으로 호출하는 메서드에 인자를 전달하지 않아도 clickBtn:function(event){} 와 같이  
      event인자를 정의하면 해당 돔 요소의 이벤트 객체에 접근 할 수 있다.
       ```js
         ...
         <button v-on:click="clickBtn">클릭</button>
         ...
         <script>
           methods: {
             clickBtn: function(event) {
                 //돔 요소의 이벤트 객체 접근 가
                 console.log(event);
             }   
           }     
         </script>
       ```
#### 고급 템플릿 기법
- `computed` 
    - 데이터 연산을 정의하는 영역으로 HTML에 데이터를 표시하기전 데이터를 가공하는 등의 연산처리를 한다.
    - computed 속성에서 사용하는 data 속성값이 변하면 자동으로 전체 값을 다시 계산한다.
    - data속성값이 변하지 않는한, 미리 연산한 결과를 가지고 있다가 필요할 때 바로 반환해준다.
    - methods vs computed
        - methods는 호출할때만 해당 로직이 수행되고, computed 속성은 해당 데이터의 값이 변경되면 자동 수행된다.
        - 복잡한 연산을 반복 수행해서 화면에 나타내야한다면 computed 속성을 이용하는 것이 성능면에서 효율적이다.
-  `watch` 
    - 데이터 변화를 감지하여 자동으로 특정 로직을 수행
    - computed는 내장 api를 활용한 간단한 연산에 적합하지만,   
        watch 속성은 데이터 호출과 같이 시간이 상대적으로 더 많이 소모되는 비동기 처리에 적합하다.
    - [예제 코드 보러가기](../5template/watch.html)
            


