<template>
  <div>
    <div v-show="dialogVisible" class="model">
      <slot></slot>
      <div class="foot">
        <input type="button" @click="modelSend" value="send">
        <input type="button" @click="boardcast" value="boardcast">
        <input type="button" @click="dialogVisible=false" value="cancel">
      </div>
    </div>
    <div v-show="dialogVisible" class="mask"></div>
  </div>
</template>

<script>
export default {
  name: 'Dialog',
  props: {
    visible: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      dialogVisible: this.visible
    }
  },
  methods: {
    modelSend () {
      this.$emit('confirm')
    },
    boardcast () {
      this.$emit('boardcast')
    }
  },
  watch: {
    visible (val) {
      this.dialogVisible = val
    },
    dialogVisible (val) {
      if (val !== this.visible) {
        this.$emit('update:visible', val) // 更新带.sync的visible。语法结构：this.$emit('update:xxxxxx', val)
      }
    }
  }
}
</script>

<style>

</style>
