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
    name: 'Scroll',
    props: {
      probeType: {
        type: Number,
        default: 0
      }
    },
    data() {
      return {
        scroll: null
      }
    },
    mounted() {
      // 1.创建BScroll对象

      // ref 如果是绑定在组件中的，那么通过 this.$refs.refname 获取到的是一个组件对象
      // ref如果是绑定在普通的元素中，那么通过 this.$refs.refname 获取到的是一个元素对象
      this.scroll = new BScroll(this.$refs.wrapper, {
        // observe-dom：开启对 content 以及 content 子元素 DOM 改变的探测。当插件被使用后，当这些 DOM 元素发生变化时，将会触发 scroll 的 refresh 方法。
        observeDOM: true,
        click: true,
        probeType: this.probeType,
        // observeImage: true
      })

      // 2.监听滚动的位置
      this.scroll.on('scroll', (position)=> {
        // console.log(position);
        this.$bus.$emit('scroll', position);  // 向外发出position
      })

      console.log(this.scroll)
    },
    methods: {
      // ES6中，若不传参数，则等于默认值
      scrollTo(x, y, time=300) {
        this.scroll.scrollTo(x, y, time)
      }
    }
  }
</script>

<style scoped>

</style>