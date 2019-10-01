
<template>

 <div id="app" style="width=100%; text-align: center;">

  <p v-if="isLoading">Loading</p>
    <search v-on:SearchRequested="handleSearch"></search>
    <preview :gifs=gifs> </preview> 
    <div style="width: 100%">
    <button @click="loadMore" style="width=500px; padding:5px;
        border:1px solid #CCC;
        background-color: #4183c4;
        color:#FFF;
        font-size:16px;
        border-radius:5px; text-align: center;" > Load More</button>
    </div> 
 
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Preview from './components/Preview.vue'  
 
export default {
  name: 'app', 
  components: { Search, Preview},

  data(){
    return{
      isLoading: true, 
      gifs: [],
      sayi:20,
      oldQuery:'',
      scrolledToBottom: false
    }
  }, 

  methods: {
    handleSearch(query){
      this.sayi=20;
      this.gifs = [];
      this.oldQuery=query;
      console.log(this.oldQuery);
      console.log(query);
      this.isLoading = true;
      fetch(`http://api.giphy.com/v1/gifs/search?q=${query}&api_key=dc6zaTOxFJmzC&limit=${this.sayi}`)
      .then((res) => {return res.json() } )
      .then((res) => {
        this.gifs = res.data;
        this.isLoading = false;
      })
    },
    loadMore(){
            this.sayi=this.sayi+20;
            console.log(this.sayi); 
            fetch(`http://api.giphy.com/v1/gifs/search?q=${this.oldQuery}&api_key=dc6zaTOxFJmzC&limit=${this.sayi}`)
              .then((res) => {return res.json() } )
              .then((res) => {
                this.gifs =res.data;
                this.isLoading =false;
              })
        },

          loadMoreScroll(){
            this.sayi=this.sayi+20;
            console.log(this.sayi); 
            fetch(`http://api.giphy.com/v1/gifs/search?q=${this.oldQuery}&api_key=dc6zaTOxFJmzC&limit=${this.sayi}`)
              .then((res) => {return res.json() } )
              .then((res) => {
                this.gifs =res.data;
                this.isLoading =false;
              })
        }

    
    },
   
  created(){
    
    fetch(`http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC&limit=${this.sayi}`)
    .then((res) => {return res.json() } )
    .then((res) => {
      this.gifs =res.data;
      this.isLoading =false;
    })

    window.addEventListener('scroll', this.loadMoreScroll);
    

  },

   beforeDestroy() {
    window.addEventListener('scroll', this.loadMoreScroll);
  }

}

</script>

<style>
#app {
  font-family:'Avenir', Helvetica,Arial,sans-serif;
  -webkit-font-something:antialiased;
  -moz-osx-font-smoothing:grayscale;
}
</style>
