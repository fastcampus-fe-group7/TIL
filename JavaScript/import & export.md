# import & export

## 모듈
개발하는 애플리케이션의 크기가 커지면 가독성과 효율을 위해 언젠간 파일을 여러 개로 분리해야 하는 시점이 온다. 이때 분리된 파일안의 개체 각각을 `모듈`이라 부르는데, 쉽게 말해 특정 함수나 클래스를 스크립트 파일 하나로 만든 것을 말한다.
이 분리된 모듈은 `import`와 `export` 지시자를 통해 이 모듈을 불러오고 내보낼 수 있다.

## export
> 다른 파일에서 현재 파일로 모듈을 내보내는 지시자

### 선언부 앞에 export 
클래스나 함수를 선언할 때, 선언부 앞에 `export`를 붙여 내보낼 수 있다.
- 사용법
  - export function 함수명(){ ... };
  ```javascript 
    //cal.js
    export function sum(a,b){
      return a + b;
    };
    export function div(a,b){
      return a / b;
    }
  ```
  - export할 함수가 여러개 선언되어 있으면 `export`를 생략한 형태로 사용할 수 있다.

  ### 선언부 밑에 export
  선언부 밑에 따로 `export`를 작성하여 내보낼 수 있다.
  - 사용법
  ```javascript
    //cal.js
    function sum(a,b){
      return a + b;
    }
    function div(a,b){
      return a / b;
    }
    export {sum, div};
  ```



## import
> 현재 파일에서 다른 파일의 모듈을 불러오는 지시자 <br>

- 사용법
  - 특정 함수만 불러오기: import {export 함수명, ... } from "파일경로";
    ```javascript
    //main.js
    import {sum} from "cal.js";

    sum(10.20);
    ```
  - 모든 함수 불러오기: import * as <obj명> from "파일 경로";
    ```javascript
    //main.js
    import * as calculator from "cal.js";

    calculator.sum(10,12);
    calculator.div(20,4);
    ``` 
  - `as`를 통해 현재 파일에서 사용할 객체 형태로 만들어 가져올 수 있다.

  ### as
  > `import`코드가 무수히 길어지는 것을 방지하기 위해 사용한다.

  - 사용법
  ```javascript
    import * as cal from "test.js";
    //import {sum, div, mul, ...} from "test.js";
  ```
  > 내보낸 모듈명을 직관적인 이름으로 사용하기 위해 선언한다.

  ### import/export 시에 선언
  - import 시에 선언
    ```javascript
      // export.js
      export function myStatus(){/*...*/}
      export function myEquipment(){/*...*/}
      export function myInventory(){/*...*/}
    ```
    ```javascript
      import {myStatus as stat, myEquipment as equip, myInventory as inven} from "export.js";
      //선언시 각각 stat/equip/inver으로 불린다.

      stat();
      equip();
      inven();  
    ```
  - export 시에 선언
    ```javascript
      //export.js
      export function myStatus(){/*...*/}
      export function myEquipment(){/*...*/}
      export function myInventory(){/*...*/}

      export {myStatus as stat, myEquipment as equip, myInventory as inven};
      //import 했을 때, 각각 stat/equip/inven으로 불린다.
    ```
    ```javascript
      import * as my from "export.js";
      //각 함수들을 my객체로 만든다.
      my.stat(...);
      my.equip(...);
      my.inven(...);
    ```

  


## export default
- `export default`는 하나의 개체만 갖고있는 모듈을 내보낼 때 선언하는 형태이다.
- `export default`는 파일 내 하나만 존재할 수 있으며, `import`시 `{}`를 사용하지 않는다. 
- 하나의 개체만 불러오면 되므로, `import`시 무엇을 불러올지 설정하지 않아도 된다.
- 또한, 개체명을 생략 가능하며 `import`시 원하는 이름으로 불러올 수 있다.

- 사용법
  ```javascript
    //user.js
    export default class user{ //user 생략가능
      constructor(name){
        this.name = name;
      }
    }
  ```
  ```javascript
    //main.js
    import anyName from "user.js"; 

    new anyName('leeyunhwan');
  ```
  - `{}`를 사용하지 않아도 자동으로 user클래스를 불러온다. 

