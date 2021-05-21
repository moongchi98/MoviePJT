## 1. 오늘의 작업

1. Login & Sign up 구현

   bootstrap 사용하기 위해서 bootstrap 설치

   ```jsx
   npm install vue bootstrap-vue bootstrap
   ```

   `index.js` 에 import 해주기

   ```jsx
   import BootstrapVue from 'bootstrap-vue'
   import 'bootstrap/dist/css/bootstrap.css'
   import 'bootstrap-vue/dist/bootstrap-vue.css'
   
   Vue.use(BootstrapVue);
   Vue.use(VueRouter)
   ```

2. Profile

   각유저의 profile 페이지를 만들기 위해서 vue페이지의 idx를 어떻게 설정해줘야하는지가 너무 어려웠다.. 특히, login과 동시에 username을 받아와서 저장하거나, 아니면 django처럼 request.user로 바로 확인하는 방법이 있는지 아직 발견하지 못햇따.

   그리고, user_id나 username을 url에 넘겨주기 위해서는 `accounts/:profile` 의 방법을 사용한다고 한다.

3. NavBar

   보통의 페이지에서는 회원가입, 로그인들의 관련 정보는 우측 상단에 위치한 다는 것을 착안하여서..  만들려고 노력했는데 vue자체의 #nav에 있는 것들에서 특정 요소만 정렬 하는 것이 매우 어려웠다. 결국 개별 div로 만들어서 margin을 통해서 위치를 조절했다

## 2. 느낀점

컨셉도 정하고, model도 만들고 나름 기능도 구현하고 많이 했다고 생각했는데 다른조랑 이야기 해보니까 엄청 맣이 한 것 같아서 마음이 조급했다.. ㅠㅠ 그리고 세세한 부분에 너무 오래 시간을 보낸 것 같아서 아쉽기도 하다

## 3. 해야 할 일

- login 시 응답값으로 username도 받아와서 profile 페이지 생성하기

  