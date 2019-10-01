<script>

new Vue({
  el: '#app',
  data: {
    loading: false,
    nextItem: 1,
    items: []
  },
  mounted () {
    const listElm = document.querySelector('#infinite-list');
    listElm.addEventListener('scroll', e => {
      if(listElm.scrollTop + listElm.clientHeight >= listElm.scrollHeight) {
        this.loadMoreScroll();
      }
    });
    
  },
 methods: {
    loadMoreScroll () {
      
      this.loading = true;
      setTimeout(e => {
        for (var i = 0; i < 20; i++) {
          this.items.push('Item ' + this.nextItem++);
        }
        this.loading = false;
      }, 200);
    }
  }*/
});


</script>