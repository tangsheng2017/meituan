<template>
  <div id="app">
    <!-- header -->
    <app-header :poiInfo='poiInfo'></app-header>
    <!-- navigation -->
    <app-nav></app-nav>
    <!-- content -->
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/header/Header'
import Nav from '@/components/nav/Nav'

export default {
  name: 'App',
  data(){
    return{
      poiInfo: {}
    }
  },
  components:{
    'app-header':Header,
    'app-nav':Nav
  },
  created(){
    this.getGoodsData()
  },
  methods:{
    getGoodsData(){
      let _this = this;

      axios.get('/api/goods')
        .then(function(response){
          _this.poiInfo = response.data.data.poi_info
          console.log(response.data.data.poi_info)
        })
    }
  }
}
</script>

<style>

</style>
