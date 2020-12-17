<template>
  <div class="hello">
    <van-search v-model="aa" :placeholder="tips"/>
    <div class="box">
      <div class="icon">
        <van-icon size="20px" name="search" @click="iconClick"/>
      </div>
      <div class="search">
        <van-swipe class="my-swipe" v-if="!stopLoop" :show-indicators="false" vertical :autoplay="playTime"
                   @change="swipeChange" indicator-color="white">
          <van-swipe-item v-for="(item,index) in arrs" :key="index" @click="itemClick">
            <input type="text" :value="item">
          </van-swipe-item>
        </van-swipe>
                <input v-if="stopLoop" type="text" ref="searchInput"
                       v-model="searchInfo.val" @blur="blurfns">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        aa: '',
        tips: '来呀',
        a1: '111111111111',
        a2: '222222222222',
        a3: '333333333333',
        playTime: 2000,
        arrs: ['11111111', '2222222', '33333'],
        itemIndex: 0,
        stopLoop: false,
        searchInfo: {
          val: ''
        }
      }
    },
    methods: {
      // focusfns(){
      // },
      blurfns() {
        let that = this
        setTimeout(() => {
          that.stopLoop = false
          that.itemIndex = 0
        }, 2000)
      },
      iconClick() {
        let val = this.searchInfo.val
        console.log(val)
      },
      itemClick(e) {
        console.log(e)
        this.stopLoop = true
        this.$nextTick( () =>{
          this.$refs['searchInput'].focus()
        })
        if (this.itemIndex === 0) {
          this.searchInfo.val = this.arrs[0]
        }
      },
      swipeChange(index) {
        console.log(index)
        this.itemIndex = index
        this.searchInfo.val = this.arrs[index]
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .box .van-icon {
    top: 10px;
  }
</style>
<style scoped>
  .my-swipe {
    overflow: hidden;
    height: 40px;
  }

  .my-swipe .van-swipe-item {
    line-height: 40px;
    text-align: center;
    /*background-color: ;*/
  }

  .box {
    width: 90%;
    height: 40px;
    margin: 0 auto;
    background: #f7f8fa;
  }

  .box > div {
    float: left;
    height: 100%
  }

  .icon {
    width: 30px;
    /*border-right: 1px solid red;*/
  }

  .search {
    width: calc(100% - 30px);
    /*border-right: 1px solid red;*/
  }

  .search input {
    width: 100%;
    height: 40px;
    padding: 0;
    border: none;
    background: transparent;
  }
</style>
