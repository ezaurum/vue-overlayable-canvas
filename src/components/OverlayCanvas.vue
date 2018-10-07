<template>
  <div class="canvas-wrapper">
    <canvas @click="clicked"></canvas>
    <div v-if="hasSlot" :class="canvasOverlayClass">
      <slot></slot>
    </div>
  </div>
</template>
<script>
import {fabric} from 'fabric'

export default {
  props: {
    image: {
      type: String,
    },
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
    overlay: {
      type: String,
      default: 'bottom',
    },
  },
  computed: {
    hasSlot() {
      return !!this.$slots.default
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
      canvas: null,
      canvasEl: null,
    }
  },
  mounted() {
    let canvasElement = this.$el.querySelector('canvas')
    this.canvasEl = canvasElement
    this.resetSize(this.width, this.height)

    let canvas = new fabric.Canvas(canvasElement)
    canvas.isDrawingMode = true;
    canvas.freeDrawingBrush.width = 5;
    canvas.freeDrawingBrush.color = "#ff0000";
    canvas.opacity = this.opacity
    this.canvas = canvas

    if (this.image) {
      fabric.Image.fromURL(this.image, (img) => {
        img.left = 0;
        img.top = 0;
        canvas.add(img);
        //img.bringToFront();
        //canvas.renderAll();
      });
      this.canvas.add()
    }
  },
  watch: {},
  methods: {
    clicked(e) {
      console.log(e)
      this.$emit('click', e)
    },
    resetSize(width, height) {
      this.canvasEl.width = width
      this.canvasEl.height = height
    },
    toDataURL() {
      return this.canvas.toDataURL('png')
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
