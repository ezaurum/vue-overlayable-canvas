<template>
  <div>
    <div class="div2">
      이 클래스는 위로 올라갈 것
    </div>
    <oc class="wrapper"
        background="yellow"
        overlay="top"
        :opacity="0.4">
      <div class="menu">
        오버레이 메뉴
      </div>
    </oc>
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
body {
  margin: 0;
  padding: 0;
}

.div1 {
  &:after {
    content: '캔버스보다 위';
  }
  background-color: red;
  width: 100%;
  height: 40px;
  color: white;
  position: absolute;
}

.wrapper {
  position: absolute;
  left: 20px;
  top: 20px;
  width: 200px;
  height: 300px;
  border-radius: 5px;
  background: #c0c0c0;
}

.div2 {
  &:after {
    content: '캔버스보다 아래';
  }
  background-color: blue;
  width: 100%;
  height: 40px;
  color: white;
}
</style>
