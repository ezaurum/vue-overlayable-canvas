<template>
  <div class="canvas-wrapper">
    <canvas></canvas>
    <div v-if="hasSlot" :class="canvasOverlayClass">
      <slot></slot>
    </div>
  </div>
</template>
<script>

export default {
  props: {
    width: {
      type: Number,
      default: 300,
    },
    height: {
      type: Number,
      default: 300,
    },
    opacity: {
      type: Number,
      default: 1,
    },
    background: {
      type: String,
      default: 'transparent',
    },
    overlay: {
      type: String,
      default: 'bottom',
    },
  },
  computed: {
    hasSlot() {
      console.log(this.$slots.default)
      return true
      /* if (!this.$slots.default) return false
       if (!this.$slots.default[0].text) return false
       if (!this.$slots.default[0].text.length) return false
       return !this.$slots.default[0].text.length*/
    },
    canvasOverlayClass() {
      return {
        'canvas-wrapper__overlay': true,
        'canvas-wrapper__overlay--bottom': this.overlay.indexOf('bottom') > -1,
        'canvas-wrapper__overlay--top': this.overlay.indexOf('top') > -1,
        'canvas-wrapper__overlay--left': this.overlay.indexOf('left') > -1,
        'canvas-wrapper__overlay--right': this.overlay.indexOf('right') > -1,
      }
    },
  },
  data() {
    return {
      canvas: Object,
      ctx: Object,
    }
  },
  mounted() {
    let canvasElement = this.$el.querySelector('canvas')
    let ctx = canvasElement.getContext('2d')
    this.canvas = canvasElement
    this.ctx = ctx
    this.canvas.style['background'] = this.background
    this.canvas.style['opacity'] = this.opacity
    this.resetSize(this.width, this.height)
  },
  watch: {
    width(to, from) {
      const width = to
      this.resetSize(width, this.height)
    },
    height(to, from) {
      const height = to
      this.resetSize(this.width, height)
    },
  },
  methods: {
    resetSize(width, height) {
      this.canvas.width = width
      this.canvas.height = height
    },
  },
}

</script>
<style lang="scss" itemscope>
.canvas-wrapper {
  position: relative;
  overflow: hidden;
}

.canvas-wrapper__overlay {
  position: absolute;
  &--top {
    top: 0;
  }
  &--bottom {
    bottom: 0;
  }
  &--left {
    left: 0;
  }
  &--right {
    right: 0;
  }
}
</style>
