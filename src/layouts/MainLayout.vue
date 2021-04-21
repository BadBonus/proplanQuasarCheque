<template>
 <div class="QuestionBlock">

   <div class="bottomBlock"></div>
   <div class="logoWrapper" :class="{logoClickQuestions:currentQuestion}">
       <img @click="chooseQuestion(!currentQuestion?'0':null, 'start')" :class="{logoClick:true}" src="~assets/statics/proplan-logo.png" alt="logo">
      <span @click="chooseQuestion(!currentQuestion?'0':null, 'start')" v-if="!currentQuestion"> <b>&#9650;</b> <br> Начать</span>
   </div>

   <img src="~assets/statics/img/dog-logo.png" alt="dog" class="animals">
   <img src="~assets/statics/img/cat-logo.png" alt="cat" class="animals cat">
    <Question @chooseQuestion="chooseQuestion" :item="currentQuestion" />

    <button v-if="currentQuestion !== null && currentQuestion.id !== '0'" @click="returnQue" class="return">
      Назад
    </button>

 </div>
</template>

<script>
import Question from 'components/Question.vue'


export default {
  name: 'MainLayout',
  components: { Question },
  data () {
    return {
      // leftDrawerOpen: false,
      // essentialLinks: linksData,
      idForLink:'',
      lastLink:'',
      currentQuestion:null,
      arrayQuestions:[{
        id:'0',
        next:['d1','c1'],
        prev:null,
        text:['для собак', 'для кошек'],
        title:'Для кого?',
        colored:false
      },
      {
        id:'c1',
        next:['c2','c8'],
        prev:'0',
        text:['да', 'нет'],
        title:'Ваш питомец старше 1 года?',
        colored:true
      },
       {
        id:'c2',
        next:['c3','c4'],
        prev:'c1',
        text:['да', 'нет'],
        title:'Есть ли питомцу 7 лет?',
        colored:true
      },
        {
        id:'c3',
        next:['l','l'],
        prev:'c2',
        text:['да', 'нет'],
        title:'Был ли стерилизован ваш питомец?',
        colored:true
      },
        {
        id:'c4',
        next:['c5','c6'],
        prev:'c2',
        text:['да', 'нет'],
        title:'Был ли стерилизован ваш питомец?',
        colored:true
      },
        {
        id:'c5',
        next:['l','l'],
        prev:'c4',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
        {
        id:'c6',
        next:['l','c7'],
        prev:'c5',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
        {
        id:'c7',
        next:['l','l'],
        prev:'c6',
        text:['да', 'нет'],
        title:'Часто линяет?',
        colored:true
      },
       {
        id:'c8',
        next:['l','l'],
        prev:'c1',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },

      {
        id:'d1',
        next:['d2', 'd8'],
        prev:'0',
        text:['да', 'нет'],
        title:'Ваша собака старше 1 года?',
        colored:true
      },
       {
        id:'d2',
        next:['d3', 'd5', 'd6'],
        prev:'d1',
        text:['Мелкая или карликовая', 'крупная', 'средняя'],
        title:'Какого размера порода вашего питомца?',
        colored:false
      },
        {
        id:'d3',
        next:['l','d4'],
        prev:'d2',
        text:['да', 'нет'],
        title:'Чувствительная кожа?',
        colored:true
      },
       {
        id:'d4',
        next:['l','l'],
        prev:'d3',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
       {
        id:'d5',
        next:['l','l'],
        prev:'d2',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
        {
        id:'d6',
        next:['l','d7'],
        prev:'d2',
        text:['да', 'нет'],
        title:'Чувствительная кожа?',
        colored:true
      },
        {
        id:'d7',
        next:['l','l'],
        prev:'d6',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
       {
        id:'d8',
        next:['l','d9', 'd11'],
        prev:'d1',
        text:['крупная', 'средняя', 'Мелкая или карликовая'],
        title:'Какого размера порода вашего питомца?',
        colored:false
      },
        {
        id:'d9',
        next:['l','d10'],
        prev:'d8',
        text:['да', 'нет'],
        title:'Чувствительная кожа?',
        colored:true
      },
      {
        id:'d10',
        next:['l','l'],
        prev:'d9',
        text:['да', 'нет'],
        title:'Чувствительное пищеварение?',
        colored:true
      },
        {
        id:'d11',
        next:['l','l'],
        prev:'d8',
        text:['да', 'нет'],
        title:'Чувствительная кожа?',
        colored:true
      },
      ]
    }
  },
    mounted(){
    if(this.$route.query.return==='true'){
      this.currentQuestion = this.arrayQuestions[0];
      this.idForLink = "0start";
    }
  },
  methods:{
    chooseQuestion(id, answ){
      console.log(id);
      if(id === null){
        this.idForLink = '';
        this.currentQuestion = null;
      }
      if(id !== null){
        this.currentQuestion = this.arrayQuestions.find(el=>el.id===id);
      this.idForLink = this.idForLink + id + answ;
      this.lastLink = id + answ;
       if(id[0]==='l'){
        this.$router.push(`/product/${this.idForLink.replace(/\s+/g, '')}`);
      }
      }

    },
    returnQue(){
      this.currentQuestion = this.arrayQuestions.find(el=>el.id===this.currentQuestion.prev);
      let newId = this.idForLink.replace(this.lastLink, '');
      this.idForLink = newId;
    }
  }
}
</script>

<style>
.QuestionBlock{
  background-color: #fff;
  position: relative;
  padding-top: 50vh;
  overflow: hidden;
  height: 100vh;
}
.bottomBlock{
  background: #000;
  height: 50vh;
}
.logoWrapper{
  width: 20%;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  height: 11vw;
}
.logoWrapper span{
  color:#fff;
     display: inline-block;
    /* background: #fff; */
    position: absolute;
    top: 21vh;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    height: 2rem;
    text-align: center;
    font-size: 1vw;
    text-transform: uppercase;
}

.logoWrapper span b {
    font-size: 1.5vw;
    position: relative;
    top:.25rem;
}

.logoClick{
width: 100%;
      border: 1px solid black;
    outline: 1px solid #fff;
    cursor: pointer;
}
.animals{
  position: absolute;
  left: 0;
  top: 0;
  height: 50vh;
}
.cat{
  left: unset;
  right: 0;
}

.logoClickQuestions{
  position: absolute;
    top: 3vh;
    bottom: unset;
    border:none;
    box-shadow: 0px 6px 6px -5px #000;
  width: 13.7%;
  height: 7.3vw;

}

.return{
  position: absolute;
  margin: auto;
  left: 0;
  right: 0;
  bottom: -43vh;
  top:0;
  background: #000;
  outline: 1px solid #fff;
  width: 11vw;
  height: 5vw;
  font-size: 2vw;
  border: none;
  color: #fff;
  box-shadow: 0 1px 6px 1px #fff;
}
</style>
