/* eslint-disable vue/return-in-computed-property */
<template>
 <div class="question" v-if="item">
     <div class="question__top"> <span>{{item.title}}</span></div>
     <div class="question__bottom">

       <button  v-for="(el, index) in item.text" @click="$emit('chooseQuestion', item.next.length === 1 ? item.next[0] : item.next[index], el)"  :key="index" :class="{...classes,
       'bg-orange':!item.colored,
       'bg-green':item.colored && index===0,
       'bg-red':item.colored}">
         {{el}}
       </button>
     </div>
   </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    item: {
      type: [Object, null],
      required: false
    },
  },
  data () {
    return({
         classes:{
      'question_variant':true,
      'q-btn':true,
      'inline':true,
      'q-btn-item':true,
      'non-selectable':true,
      'no-outline':true,
      'q-btn--standard':true,
      'q-btn--rectangle':true,
      'text-white':true,
      'q-focusable':true,
      'q-hoverable': true
    }})
  },

  computed: {

  },
}
</script>

<style>
.question{
      position: absolute;
    top: 0;
    bottom: 0;
    margin: auto;
    left: 0;
    right: 0;
    background: #000;
    width: 50vw;
    height: 14vw;
        border-radius: 4px;
}
.question>*{
  position: absolute;
  height: 50%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.question__top{
  top: 0;
}
.question__top span{
  color: #fff;
  font-size: 2.5vw;

}
.question__bottom{
  background: #fff;
  bottom: 0;
  justify-content: space-evenly;
  border-radius: 0 0 4px 4px;
}
.question button{
    width: 11vw;
    height: 4vw;
    min-height: 2.572em;
    box-shadow: 0 1px 5px rgb(0 0 0 / 20%), 0 2px 2px rgb(0 0 0 / 14%), 0 3px 1px -2px rgb(0 0 0 / 12%);
    font-size: 1.2vw;
    display: flex;
    justify-content: center;
}
</style>
