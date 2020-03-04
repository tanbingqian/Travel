<template>
  <div>
    <div
      class="item"
      v-for="(item, index) of list"
      :key="index"
     >
      <div class="item-title border-bottom">
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <div v-if="item.children" class="item-children">
        <deatil-list :list="item.children"></deatil-list>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'deatilList',
  props: {
    list: {
      type: Array
    }
  },
  data () {
    return {
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .item-title-icon
    position: relative
    left: .06rem
    top: .06rem
    display: inline-block
    width: .36rem
    height: .36rem
    background: url(https://pic.c-ctrip.com/VacationH5Pic/group_travel/index/mendian.png) 0 -.45rem no-repeat
    margin-right: .1rem
  .item-title
    line-height: .8rem
    font-size: .32rem
    padding: 0 .2rem
  .item-children
    padding: 0 .12rem
</style>
