<template>
  <div>
    <deatil-banner
      :sightName="sightName"
      :bannerImg="bannerImg"
      :bannerImgs="gallaryImgs"
      :list="list"
    ></deatil-banner>
    <deatil-header></deatil-header>
    <div class="centent">
      <deatil-list :list="list"></deatil-list>
    </div>
  </div>
</template>

<script>
import DeatilBanner from './components/Banner'
import DeatilHeader from './components/Header'
import DeatilList from './components/List'
import axios from 'axios'
export default {
  name: 'Deatil',
  data () {
    return {
      sightName: '',
      bannerImg: '',
      gallaryImgs: [],
      list: []
    }
  },
  methods: {
    getDetailInfo () {
      axios.get('./api/detail.json', {
        params: {
          id: this.$route.params.id
        }}
      ).then(
        this.getDetailSucc
      )
    },
    getDetailSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.sightName = data.sightName
        this.bannerImg = data.bannerImg
        this.gallaryImgs = data.gallaryImgs
        this.list = data.categoryList
      }
    }
  },
  activated () {
    this.getDetailInfo()
  },
  components: {
    DeatilBanner,
    DeatilHeader,
    DeatilList
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .centent
    height: 14rem
</style>
