<template>
  <div class="wrapper" @click="showElse">
    <header>
      <span></span>
      <section class="avatar">
        <div class="tools">
          <!--<img class="iconfont tool" src="~assets/img/header-tool.png"/>-->
          <i class="material-icons">blur_on</i>
          <section class="tools-items">
            <ul>
              <li>
                <a href="">
                  <img src="" alt="">
                  <p>词云</p>
                </a>
              </li>
            </ul>
          </section>
        </div>
        <div class="user" @click.stop="openUser">
          <!--<img class="head" src="~assets/img/header-heads.png" alt="头像">-->
          <i class="material-icons">person</i>
          <div class="user-panel " v-show="openU">
            <section class="arrow"></section>
            <ul>
              <li class="login-in"><a href="/login/">登录</a></li>
              <li><a href="/plan/" target="_blank">定制服务</a></li>
              <li class="subscribe" style="display: none"><a href="/app/#/oldAlerts" target="_blank">已创建的订阅</a></li>
              <li class="log-out" style="display: none">登出</li>
            </ul>
          </div>
        </div>
      </section>
    </header>
    <div class="containers">
      <section class="logo">
        <header>
          <div class="img">
            <img src="~assets/img/logo3.png" alt="LOGO">
          </div>
          <h3>MAOPING SHOU</h3>
          <p>猫评数据</p>
        </header>
      </section>
      <section class="zone">
        <section class="inner">
          <input type="text" id="search" placeholder="" v-model="searchText" @blur="closeSearch" @focus="openSearch">
          <i class="iconfont to-go" title="点击搜索" @click="searchList">></i>
          <section class="simulation" ref="simulation">中国</section>
        </section>
        <p>大众评论分析利器</p>
      </section>
      <section class="advise none"></section>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import {mapGetters, mapMutations} from 'vuex'

  export default {
    created () {
      console.log(this.loginState)
    },
    data () {
      return {
        searchText: '',
        login: false,
        openU: false
      }
    },
    computed: {
      ...mapGetters([
        'loginState'
      ])
    },
    components: {},
    watch: {
      searchText (newVal, oldVal) {
      }
    },
    methods: {
      openSearch () {
        this.$refs.simulation.style.display = 'none'
      },
      closeSearch () {
        if (this.searchText === '') {
          this.$refs.simulation.style.display = 'block'
        }
      },
      searchList () {
        let userText = this.searchText
        console.log(userText)
        console.log('跳')
        this.setSearchList = userText
        this.$router.push({path: `/app/${userText}`})
      },
      openUser (e) {
        e.preventDefault()
        this.openU = !this.openU
      },
      showElse () {
        if (this.openU) {
          this.openU = !this.openU
        }
      },
      ...mapMutations({
        setSearchList: 'SET_SEARCHLIST'
      })
    }
  }
</script>


<style scoped lang="stylus" rel="stylesheet/stylus">

  .wrapper
    display: flex
    justify-content: center
    flex-wrap: wrap
    height 85%
    header
      display: flex
      justify-content: space-between
      width: 100%
      text-align: right
      padding 0 40px
      max-height: 100px
      .avatar
        display flex
        justify-content: center
        align-items: center
        flex-wrap: wrap
    .containers
      text-align: center
      position: relative
      margin-bottom: 150px
      .logo
        margin-bottom: 50px
        header
          display: block
          position: relative
          z-index: 0
          p
            text-align: center
            font-size: 12px
            color: #9b9b9b
            margin-top: 8px
          h3
            text-align: center
            font-size: 13px
            color: #4a4a4a
            margin-top: 20px
          .img
            -webkit-border-radius: 50%
            -moz-border-radius: 50%
            border-radius: 50%
            position: relative
            height: 50px
            width: 50px
            margin: 0 auto
            background-color: #498bfb
            display: flex
            align-items: center
            justify-content: center
            img
              height: 100%
              width: 100%
          .img:after
            content: ""
            display: block
            position: absolute
            width: 25px
            height: 25px
            border-radius: 50%
            backrgound-color: #8fb1e9
            filter: blur(3px)
            left: 50%
            top: 41px
            transform: translate(-50%, -50%)
            z-index: -1
    .zone
      margin-bottom: 50px
      p
        font-size: 13px
        color: #9b9b9b
        font-weight: lighter
      .inner
        position: relative
        margin-bottom: 15px
        input
          width: 400px
          height 48px
          background: #fff
          color: #4a4a4a
          box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, .12)
          border-radius: 4px
          border: none
          outline: none
          padding: 0 15px
          font-size: 24px
          font-weight: lighter
          text-align: center
        .to-go
          position: absolute
          width: 50px
          height: 100%
          line-height: 48px
          right: 0
          top: 0
          cursor: pointer
          color: #9b9b9b
          transition: all .25s
          font-size: 30px
        .to-go:hover
          background: #e2455b
          color: #fff
      .simulation
        height: 100%
        line-height: 48px
        background: #fff
        position: absolute
        top: 0
        left: 50%
        transform: translateX(-50%)
        color: #cccccc
        font-style: italic
        font-size: 13px
        font-weight: lighter
      .simulation:after
        content: " "
        display: block
        height: 35%

  .title
    font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif /* 1 */
    display: block
    font-weight: 300
    font-size: 100px
    letter-spacing: 1px

  .tools
    position: relative
    cursor: pointer
    .tools-items
      display none
      z-index: 9999
      width 300px
      right: -30px
      top: 40px

  .arrow
    position: absolute
    width: 13px
    height: 13px
    background-color: #fff
    transform: rotate(45deg) translateX(-50%)
    top: -2px
    border: 1px solid #c5c5c6
    border-right: none
    border-bottom: none

  .user
    margin-left: 35px
    position: relative
    .user-panel
      position: absolute
      text-align: left
      font-size: 13px
      color: #4a4a4a
      width: 150px
      top: 50px
      right: -2px
      z-index: 999
      ul
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, .12)
        border: 1px solid #c5c5c6
        border-radius: 4px
        padding: 10px
        position: relative
        cursor: pointer
        z-index: 1
        right: -10px
        li
          line-height: 2.5
          a
            color: #4a4a4a
            text-decoration: none
      .arrow
        right: 3px
        z-index: 2


</style>
