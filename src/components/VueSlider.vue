<template>
  <div class="vue-slider">
    <div class="vue-slider-wrapper" ref="wrapper">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: 'VueSlider',
  props: {
    options: {
      required: true,
      type: Object
    },
    list: {
      required: true,
      type: Array
    }
  },
  data () {
    const { perView = 3, autoplay = false, loop = false } = this.options
    return {
      perView,
      autoplay,
      loop,
      lastTransX: 0
    }
  },
  mounted () {
    this.init()
  },
  watch: {
    'list.length': {
      handler () {
        this.$nextTick(() => {
          this.init()
        })
      },
      deep: true
    }
  },
  methods: {
    init () {
      this.calItemWidth()
      this.moveWrapper()
    },
    calItemWidth () {
      let wrapper = this.$refs.wrapper
      let len = wrapper.children.length
      for (let i = 0; i < len; i++) {
        let child = wrapper.children[i]
        child.style.width = (1 / this.perView * 100).toFixed(5) + '%'
        child.style.display = 'inline-block'
      }
    },
    moveWrapper () {
      let wrapper = this.$refs.wrapper
      let len = wrapper.children.length
      let childWidth = Number((this.$el.offsetWidth * (1 / this.perView)).toFixed(5))
      let x = this.lastTransX
      if (this.timer) {
        clearInterval(this.timer)
        this.timer = null
      }
      this.timer = setInterval(() => {
        wrapper.style.transform = `translateX(-${x}px)`
        x += childWidth
        if (x > (len - this.perView) * childWidth) {
          x = 0
        }
        this.lastTransX = x
      }, 2000)
    }
  }
}
</script>
<style lang="scss" scoped>
.vue-slider {
  height: 100%;
  width: 100%;
  overflow: hidden;
  box-sizing: border-box;
}
.vue-slider-wrapper {
  height: 100%;
  box-sizing: border-box;
  white-space: nowrap;
  transition-duration: 600ms;
}
</style>
