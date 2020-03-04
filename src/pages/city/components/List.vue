<template>
    <div class="list" ref="wrapper">
      <div>
        <div class="area">
            <div class="title border-topbottom">当前城市</div>
            <div class="button-list">
            <div class="button-wrapper">
                <div class="button">{{this.currentCity}}</div>
            </div>
            </div>
        </div>
        <div class="area">
            <div class="title">热门城市</div>
            <div class="button-list">
                <div
                  class="button-wrapper"
                  v-for="item of hot"
                  :key="item.id"
                  @click="handleCityClick(item.name)"
                >
                  <div class="button">{{item.name}}</div>
                </div>
            </div>
        </div>
        <div class="area"
          v-for="(item,key) in cities"
          :key="key"
          :ref="key"
        >
            <div class="title border-topbottom">{{key}}</div>
            <div class="item-list"
              v-for="innerItem of item"
              :key="innerItem.id"
              @click="handleCityClick(innerItem.name)"
            >
              <div class="item border-bottom">{{innerItem.name}}</div>
            </div>
        </div>
      </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    cities: Object,
    hot: Array,
    letter: String
  },
  computed: {
    ...mapState(
      {
        currentCity: 'city'
      }
    )
  },
  watch: {
    letter () {
      const element = this.$refs[this.letter][0]
      this.scroll.scrollToElement(element)
    }
  },
  methods: {
    handleCityClick (city) {
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    // const options = {
    //   click: true,
    //   tap: true
    // }
    this.scroll = new Bscroll(this.$refs.wrapper, {click: true})
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .border-topbottom
    &:before
      border-color: #cccccc
    &:after
      border-color: #cccccc
  .border-bottom
    &:before
      border-color: #cccccc
  .list
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
  .title
    line-height: .54rem
    background: #eee
    padding-left: .2rem
    color: #666
    font-size: .26rem
  .button-list
    padding: .1rem .6rem .1rem .1rem
    overflow: hidden
    .button-wrapper
      float: left
      width: 33.33%
      .button
        margin: .1rem
        padding: .1rem 0
        text-align: center
        border: .02rem solid #ccc
  .item-list
    .item
      line-height: .76rem
      padding-left .2rem
</style>
