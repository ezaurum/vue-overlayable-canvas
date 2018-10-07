<template>
  <div>
    <div class="div2">
      이 클래스는 위로 올라갈 것
    </div>
    <oc></oc>
    <div class="div1">
      이 클래스는 뒤로 들어갈 것
    </div>
  </div>
</template>
<script>
import oc from '@/components/OverlayCanvas'

export default {
  components: {
    oc,
  },
}
</script>
<style lang="scss">
.div1 {
  &:after {
    content: '캔버스보다 위';
  }
  background-color: red;
  width:100%;
  height:40px;
  color:white;
}

.div2 {
  &:after {
    content: '캔버스보다 아래';
  }
  background-color: blue;
  width:100%;
  height:40px;
  color:white;
}
</style>
