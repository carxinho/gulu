<template>
  <div class="tabs-head">
    <slot></slot>
    <div class="line" ref="line"></div>
    <div class="actions-wrapper">
      <slot name="actions"></slot>
    </div>
  </div>
</template>
<script>
export default {
  name:'WheelTabsHead',
  inject: ["eventBus"],
  mounted() {
    this.eventBus.$on('update:selected', (item, vm) =>{
      if (vm) {
        let {width, height, top, left} = vm.$el.getBoundingClientRect()
        let parentLeft = vm.$parent.$el.getBoundingClientRect().left
                console.log(parentLeft)
        this.$refs.line.style.width = `${width}px`
        this.$refs.line.style.left = `${left - parentLeft}px`
      }
    })
  }
};
</script>
<style lang="scss" scoped>
$tab-height: 40px;
$blue:blue;
$border-color:#ddd;
.tabs-head {
  position: relative;
  display: flex;
  justify-content: flex-start;
  height: $tab-height;
  border-bottom: 1px solid $border-color;
  .actions-wrapper{
    margin-left: auto;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0 1em;
  }
  .line{
    position: absolute;
    bottom: 0;
    border-bottom: 2px solid $blue;
    transition: all 350ms;
  }
}
</style>
