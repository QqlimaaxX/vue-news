<template>
  <div id="app" class="container">
    <source-selection v-on:sourceChanged="sourceChanged"></source-selection>
    <news-list :source="source"></news-list>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import NewsList from './components/NewsList'

export default {
    name: 'app',
    components:{
      SourceSelection,
      NewsList
    },
    data(){
      return{
        source:"",
      }
    },
    methods:{
      sourceChanged:function(source) {
          console.log("Signal Received")
          console.log(source);
          this.source = source;
        }
      }
  }

</script>

<style>

#app {
    padding-top: 20px;
}

</style>
