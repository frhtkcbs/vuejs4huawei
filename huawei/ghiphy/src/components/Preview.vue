

<template>
        <div style="width:40%  height:auto; text-align: center; padding:15px; margin:15px;">
            <ul>
                <li v-for="gif in gifs" style="width:100%">
                    <img :src="gif.images.fixed_height.url"/>
                </li>
            </ul>
        </div>
</template>


<script>
 export default{
        props:['gifs']
    }

</script>
   
<style>
    ul{
        display: inline-block;
        margin-left: auto;
        margin-right: auto;
        text-align: center;
    }

    li {
       list-style:none;
        margin-left: 15px;
        margin-right: 15px; 
    }

</style>