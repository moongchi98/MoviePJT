## 오늘 한 작업

### Movies

1. `Home.vue`: 영화 정보를 보여주는 Main Page

   모든 영화 list를 보여줌

2. `MovieItem.vue` : 메인 페이지에서 개별 영화를 li요소로 나타내기 위한 페이지

   ⇒ 상세 페이지랑은 다름

### Community

1. `Community` : 전체 review 제목들을 나타내는 페이지
2. `ReviewListItem` : 전체 목록을 위한 list 아이템
3. `ReviewCreate` : 게시글 작성을 위한 페이지
4. 🌟`ReviewDetail` : 개별 review 상세 정보를 위한 페이지

### Review Detail ⇒ 동적 라우팅 `:` 을 사용하다!

django에서처럼 url에 개별 reivew의 id를 넘겨준 식으로 detail url을 구성하기 위해서 진짜 많은 애를 먹었따.. 눈물 광광 ;ㅂ;,,, `:` 나, children을 사용한다고만 나와있고 구체적으로 사용방법을 몰랐는데 병현형님이 도와주셨다...정말 압도적 감사..

우선 review page를 이를 사용해서 구현을 성공했기 때문에 내일부터는 movie, profile도 문제 없이 만들 수 있을 것 같다.

1. index.js 에 router 설정하기

```jsx
//index.js
{
    path:'/memovies/community/:reviewId',
    name:'ReviewDetail',
    component: ReviewDetail,
    props: true,
  }
```

내가 변하면서 주고 싶은 값에다가 : 를 설정해줘야 한다! 우리는 reviewId값을 변화를 주고 싶기 때문에 다음과 같이 설정하였다. 또한, `props:true` 를 설정하게 되면 우리가 params로 전달해준 data를 props로 받아올 수 있다고 한다.

1. Community(상위)에서 연결해주기

```jsx
<template>
  <div>
    <h1>Review 게시판</h1>
    <button @click="onClick">리뷰작성</button>
    <ul>
      <ReviewListItem v-for="review in reviews" :key="review.id" :review="review" @click.native="getReview(review.id)" v-text="review.title"/>
    </ul>
  </div>
</template>
<script>
import axios from 'axios'
import ReviewListItem from '@/views/community/ReviewListItem'
export default {
  name:'Community',
  components:{
    ReviewListItem,
  },
	methods:{
    getReview(reviewId){
      this.$router.push({ name:'ReviewDetail', params:{ reviewId:reviewId }})
    }
  },
}
</script>
```

상세페이지로 넘어가는 방법은 다음과 같다

1. 우선 ReviewListItem.vue를 만들어서 개별 게시글을 li 태그로 만든다.

   ✨ 이게 진짜 중요한데, 처음에 community에서 전체적으로 보여주는 아이템이랑, 상세페이지랑 같이 설정하려고 하니까 계속 에러가 발생했다. 즉, listitem은 정말로 전체 페이지에서 보여주기 위한 역할만 하고, `ReviewDetail` 에서 따로 상세정보를 보여 줘야 한다!!

2. 불러온 ReviewListItem을 클릭할 경우에는 ⇒ router.push를 통해서 detail페이지로 이동시킨다!!

   **❤️ 여기서 왕 중요 포인트!~!!!!**

   **우리가 변하는 값을, `params:{reviewId:reviewId}` 로 전해주면 된다. 이때, reviewId란 값은 click이벤트가 발동했을때 실행시키는 함수의 인자로 전달되는 값이다.**

3. 최종 개별 Detail Page

   url을 설정했는데 ^^,, 데이터가 안보인다~!~! 의 큰 산이 남았었다. 도대체 전달해주는 reviewId를 어떻게 받아올까? 였는데, 그 방법은 **`this.$router.params.reviewId`**이 방식이다!!!!

   ```jsx
   // ReviewDetail.vue
   <template>
   <!-- 영화별 상세 정보 page -->
     <div class="font">
       <h1>{{ review.title }}</h1>
       <p>영화 : {{ review.movie_title }}</p>
       <p>내용: {{ review.content }}</p>
       <p>작성일: {{ review.created_at }}</p>
     </div>
   </template>
   
   <script>
   import axios from 'axios'
   export default {
     name:'ReviewDetail',
     data(){
       return{
         review:[],
       }
     },
     created(){
       axios({
         url:`http://127.0.0.1:8000/memovies/community/reviews/`+this.$route.params.reviewId,
         method:'get',
       })
         .then(res=>{
           console.log(res)
           this.review = res.data
         })
     },
   
   }
   </script>
   
   <style>
   
   </style>
   ```

## 느낀 점

오늘의 느낀점이라...하믄.........빈산쌤이 왜 vue쓰면 어렵다고 하는지..................백천만배이해.............. 그런데 동적 라우팅하고 어찌저찌 구현하니가 너무 뿌듯하다ㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠ사실 난 천재가 아닐까..? 이런 착각에 빠졌다..