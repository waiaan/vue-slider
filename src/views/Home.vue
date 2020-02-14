<template>
  <div class="home">
    <div class="wrapper">
      <vue-slider :options="options" :list="list">
        <div v-for="(item,index) in list" :key="index" style="border:1px solid;box-sizing:border-box;">
          {{item}}
        </div>
      </vue-slider>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import VueSlider from '@/components/VueSlider'

export default {
  name: 'home',
  components: {
    VueSlider
  },
  data () {
    return {
      list: [1, 2, 3, 4, 5, 6],
      options: {
        perView: 3,
        autoplay: true,
        loop: true
      }
    }
  },
  mounted () {
    setTimeout(() => {
      this.list.push(7)
    }, 5000)
  }
}
</script>
<style lang="scss" scoped>
.wrapper {
  width: 500px;
  height: 200px;
  margin: 0 auto;
}
</style>
