<template>
 <div class="QuestionBlock">

   <div class="bottomBlock"></div>
   <img @click="chooseQuestion(!currentQuestion?'0':null, 'start')" :class="{logoClick:true,
   logoClickQuestions:currentQuestion}" src="~assets/statics/proplan-logo.png" alt="logo">
   <img src="~assets/statics/img/dog-logo.png" alt="dog" class="animals">
   <img src="~assets/statics/img/cat-logo.png" alt="cat" class="animals cat">
    <Question @chooseQuestion="chooseQuestion" :item="currentQuestion" />

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
        next:['d2', 'd5'],
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
        colored:true
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
  methods:{
    chooseQuestion(id, answ){
      this.currentQuestion = this.arrayQuestions.find(el=>el.id===id);
      this.idForLink = this.idForLink + id + answ;
       if(id[0]==='l'){
        this.$router.push(`/product/${this.idForLink.replace(/\s+/g, '')}`);
      }
    }
  }
}
</script>

<style>
.QuestionBlock{
  background-color: #fff;
  position: relative;
  padding-top: 50vh;
}
.bottomBlock{
  background: #000;
  height: 50vh;
}
.logoClick{
  width: 20%;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
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

}


</style>
