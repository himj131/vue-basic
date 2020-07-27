# Vue 인스턴스 라이프사이클

1. 인스턴스 생성(new Vue())  
    1-1. 이벤트및 라이프 사이클 초기화 
    1-2. beforCreate
    1-2. 화면에 반응성 주입
    1-3. created
    1-4. el, template 속성확인
    1-5. template 속성 내용을 render()로 변환
    1-6. beforeMount
    1-7. $el 생성 후 el 속성 값을 대입
    1-8. mounted

2. 인스턴스를 화면에 부착  
    2-1. (데이터가 변경되는 경우에) 인스턴스의 데이터 변경
    2-2. (데이터가 변경되는 경우에) beforeUpdate
    2-3. (데이터가 변경되는 경우에) 화면 재 렌더링 및 데이터 갱신
    2-4. updated

3. 인스턴스 내용 갱신
    3-1. 인스턴스 접근 가능
    3-2. beforeDestory
    3-3. 컴포넌트, 인스턴스, 디렉티브 등 모두 해제
    3-4. destroyed
    
4. 인스턴스 소멸
