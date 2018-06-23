<template>
  <div id="app">
    <!-- header -->
    <app-header :poiInfo='poiInfo'></app-header>
    <!-- navigation -->
    <app-nav :commentNum='commentNum'></app-nav>
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
      poiInfo: {},
      commentNum:0
    }
  },
  components:{
    'app-header':Header,
    'app-nav':Nav
  },
  created(){
    this.getGoodsData()

    // 请求ratings
    fetch("/api/ratings")
      .then(res => {
        return res.json()
      })
      .then(response =>{
        if(response.code == 0){
          this.commentNum = response.data.comment_num
        }
      })
  },
  methods:{
    getGoodsData(){
      let _this = this;

      axios.get('/api/goods')
        .then(function(response){
          _this.poiInfo = response.data.data.poi_info
        })
    }
  }
}
</script>

<style>

</style>
