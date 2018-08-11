<template>
  <div>
    <add-post></add-post>
  </div>
</template>

<script>

import addPost from './components/addPost.vue';

export default {
  //register the componetn
  components:{
    'add-post':addPost
  },

  data(){
    return{

    }
  }, 
  methods:{

  }
}
</script>

<style>
  body{
    margin: 0;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif
  }
</style>
