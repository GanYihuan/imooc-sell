<template>
  <div class="cartControl">
    <transition name="move">
      <div
        class="cart-decrease"
        v-show="food.count>0"
        @click.stop.prevent="decreaseCart"
      >
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <span class="cart-count" v-show="food.count>0">{{food.count}}</span>
    <span class="cart-add icon-add_circle" @click.stop.prevent="addCart"></span>
  </div>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue'

export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart(event) {
      if (!event._constructed) {
        return
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1) /* add food attribute count=1 */
      } else {
        this.food.count++
      }
      this.$emit('add', event.target)
    },
    decreaseCart(event) {
      if (!event._constructed) {
        return
      }
      if (this.food.count !== 0) {
        this.food.count--
      }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
@import 'cartControl.scss';
</style>
