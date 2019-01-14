<template>
  <div v-color="elementColor" class="content">
    <div class="number">{{elementNumber}}</div>
    <div class="abv">{{elementAbv}}</div>
    <div class="name">{{elementName}}</div>
  </div>
</template>

<script>
export default {
  props: {
    elementName: {required: true},
    elementAbv: {required: true},
    elementNumber: {required: true},
    elementColor: {required: true}
  },
  // props: ['elementName', 'elementAbv', 'elementNumber', 'elementColor'],
  directives: {
    color (el, binding){
      el.style.border = '1px solid #' + binding.value
    }
  }
}
</script>

<style lang="scss">
.content{
  display: inline-block;
  border: 1px solid blue;
  width: 70px;
  height: 70px;
  margin: 10px 5px;
  position: relative;
  .number{
    position: absolute;
    top: 0;
    left: 3px;
  }
  .abv{
    position: absolute;
    top: 50%;
    left: 50%;
    font-size: 25px;
    font-weight: bold;
    transform: translate(-50%, -50%);
  }
  .name{
    position: absolute;
    bottom: 0;
    left: 3px;
    font-size: 10px;
  }
}
</style>
