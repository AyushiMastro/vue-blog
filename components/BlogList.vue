<template>
  <div>
    <h1>hlw list</h1>
  </div>
</template>
<script>
import Vue from 'vue';
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios.axios)
export default{
    name="BlogList",
    mounted(){
        Vue.axios.get('https://jsonplaceholder.typicode.com/todos/1'
        )
            console.warn(res)
        })
    }
}
</script>
