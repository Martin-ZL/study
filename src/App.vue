<template>
  <div class="vueApp">
    <v_header :seller="seller"></v_header>
    <div class="tab border-1px">
      <div class="tab_item">
        <router-link to="/goods">
          商品
        </router-link>
      </div>
      <div class="tab_item">
        <router-link to="/ratings">
          评价
        </router-link>
      </div>
      <div class="tab_item">
        <router-link to="/seller">
          商家
        </router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from 'components/header/header'

  export default {
    data() {
      return {
        seller: {}
      }
    },
    created() {
      // GET /api/seller
      this.$http.get('/api/seller').then(response => {
          // get body data
        response = response.body
        if (response.errno === 0) {
          this.seller = response.data
        }
      }, response => {
          // error callback
      })
    },
    components: {
      v_header: header
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "common/stylus/mixin.styl";

  .vueApp{
    height: 100%;
    .tab{
      display: flex;
      width:100%;
      border-1px(rgb(7,17,27));
      .tab_item{
        flex:1;
        text-align: center;
        height: 40px;
        line-height: 40px;
        &>a{
            display: block;
            &.tab_active{
               color: rgb(240,20,20);
             }
          }
      }
    }
  }
</style>
