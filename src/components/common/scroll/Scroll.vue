<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name:"Scroll",
  props: {
    probeType: {
      type:Number,
      default:0
    },
    pullUpLoad: {
      type: Boolean,
      default:0
    }
  },
  data() {
    return {
      scroll:null
    }
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper,{
      observeDOM:true,
      click:true,
      probeType:this.probeType,
      pullUpLoad:this.pullUpLoad
    })

    //监听滚动
    this.scroll.on('scroll',postion => {
      this.$emit('scroll',postion)
    })

    //监听上拉
    this.scroll.on('pullingUp',() => {
      this.$emit('pullingUp')
    }) 
  },
  methods: {
   scrollTo(x,y,time = 300) {
     this.scroll.scrollTo(x, y, time)
   },
   finishPullUp() {
     this.scroll.finishPullUp()
   }
  }
}
</script>

<style scoped>

</style>