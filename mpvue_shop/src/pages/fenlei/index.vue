<template>
  <div class="fenlei">
    <div>
      <div class="fenlei_top">
        <div class="fenlei_top_left">
          <input type="text" placeholder="搜索商品" class="ins">
        </div>
        <div class="fenlei_top_right">
          搜索
        </div>
      </div>
      <div>
        <div class="fenlei_content">
          <scroll-view :style="{'height': '100vh'}" scroll-y>
            <div class="leftwrapper">
              <div class="fenlei_content_left">
                <span :class="['xinpin' ,{showtab:tabindex==index}]" v-for="(item,index) in tablists" :key="index"
                  @click="Switch(index)">
                  {{item.category_name}}
                </span>
              </div>
            </div>
          </scroll-view>
          <scroll-view :style="{'height': '100vh'}" scroll-y>
            <div class="wrapper">
              <div>
                <div class="fenlei_content_right" v-if="catelist">
                  <div class="fenlei_content_items" v-for="(imgs,index) in catelist" :key="index" @click='godetails(imgs.id)'>
                    <div class="imgs">
                      <img v-bind:src="imgs.img" alt="">
                    </div>
                    <span class="items_name">
                      小米手机
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </scroll-view>
        </div>
      </div>
    </div>
    <!-- 底部组件 -->
  </div>
</template>

<script>
    export default {
      // 开始
      components: {

      },
      // 结束
      name: 'fenlei',
      data: function () {
        return {
          newTitle: '商品分类',
          tabindex: '0',
          url: 'https://www.easy-mock.com/mock/59e95287dd7e1a0a448c1102/example/fenlei',
          catelist: '',
          tablists: ''
        }
      },
      created () {
        console.log('created')
        var _this = this
        this.$http.get(_this.url).then(function (res) {
          console.log(res.data)
          _this.tablists = res.data
          _this.catelist = res.data[0].cateitems
        })
      },
      mounted () {
        this.tabindex = 0
      },
      methods: {
        //  切换tab
        Switch: function (index) {
          var _this = this
          _this.tabindex = index
          console.log(index, 'index')
          _this.catelist = _this.tablists[index].cateitems
        },
        // 详情
        godetails: function (id) {
          wx.navigateTo({
            url: '/pages/details/main?id=' + id
          })
        }
      }
    }
</script>

<style scoped>
    body {
        touch-action: none
    }
    
    .showtab {
        color: red;
        border-bottom: 1px solid red;
        /* animation: mymove 1s 1; */
        background: #fff;
        /* -webkit-animation: mymove 1s 1; */
    }
    
    @keyframes mymove {
        from {
            font-size: 0.4rem;
            transform: scale(0.3);
        }
        to {
            font-size: 0.32rem;
            transform: scale(0.5);
        }
    }
    
    body {
        background: #eee;
    }
    
    .ins {
        border: 0;
        outline: none;
        width: 5.5rem;
        padding: 0.2rem;
    }
    
    .fenlei_top_left {
        width: 5.5rem;
        padding: 0.2rem 0;
    }
    
    .fenlei_top {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 0.88rem;
        padding: 0.1rem 0.2rem;
        width: 95vw;
        background: #eeeeee;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 99;
    }
    
    .fenlei_top_right {
        font-size: 0.32rem;
        color: #353535;
        width: 1rem;
        text-align: center;
    }
    
    .fenlei_content {
        background: #fff;
        display: flex;
        margin-top: 100rpx;
        overflow: hidden;
    }
    
    .fenlei_content_left {
        width: 30vw;
        background: #eee;
        font-size: 0.32rem;
        color: #353535;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
        /* overflow-x: scroll; */
    }
    
    .fenlei_content_right {
        width: 65vw;
        background: #fff;
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 0 0.2rem 0.2rem 0.2rem;
        /* overflow-x: scroll; */
    }
    
    .fenlei_content_items {
        /* padding: 0.1rem; */
        border: 1px solid #eee;
        box-shadow: 0.1rem 0.1rem 0.1rem #353535;
        margin-top: 0.2rem;
    }
    
    .imgs {
        width: 2.3rem;
        height: 3rem;
        padding: 0.2rem 0;
    }
    
    .imgs img {
        width: 100%;
        height: 100%;
    }
    
    .items_name {
        font-size: 0.32rem;
        color: #353535;
        text-align: center;
        width: 100%;
        display: inline-block;
        margin-top: 0.1rem;
    }
    
    .xinpin {
        display: inline-block;
        text-align: center;
        width: 100%;
        padding: 0.2rem 0;
    }
</style>