## JSP

#### Explore 개발자 모드에서만 실행되는 오류



###### 로컬환경에서 열심히 개발과 테스트를 하고서 테스트 서버에 소스들을 배포했다. 그러고서 Explore로 실행하는데... ???????? 버튼 ```onClick``` 이벤트가 실행이 안된다..;; 아예 먹통..

###### 로깅을 하려고 console.log(); 를 확인해보려고 F12를 눌러 ```개발자모드``` 를 실행시키고 다시 한번 눌렀는데??? 실행이 된다.

###### onClick을 바꿔보고 ```$(function() { $("#buttonId").click() {}}``` 으로 변경도 해봤는데 오류를 찾을 수 없었다...

##### 그러던 중 IE9 이상 버전 부터 window.console을 null로 인식하며 개발자 모드를 실행시켜야지만 제대로인식을 하고 실행이 가능한 것..!



###### console.log(); 를 모두 제거하고 실행하니 정상적으로 실행이 됐다 乃



###### 불가피하게 console.log()를 넣어야 하는 경우는 아래처럼 조건을 적용하면 오류를 방지할 수 있다

```javascript
if(window.console != null){
    console.log("로깅");
}
```



### 마치며

###### 정말 이해 하지 못할 오류들도 그 오류가 발행한 원인이 있고 원인을 해결할 수 있는 방안이 있는 것 같다. 진짜 말도 안된다는 오류라고 생각했다. F12를 눌러야만 실행이 된다니;; 

###### 그래도 이렇게 말도 안되는 것도 하나하나 해결하는 것이 좀 속이 시원하기도 하고 몰랐다면 또 언젠간 발생할 오류가 아니었을까! 