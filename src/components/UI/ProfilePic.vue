<template>
  <div>
      <img v-bind:width="width" v-bind:class="{full: full}" @error="onError" v-bind:height="height" v-bind:src="accIcon" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'ProfilePic',
  props: {
    width: {
      type: Number,
      default: 50
    },
    height: {
      type: Number,
      default: 50
    },
    full: {
      type: Boolean,
      default: false
    }
  },
  computed: mapGetters(['accIcon', 'failIcon']),
  methods: {
    onError () {
      this.$store.commit('setIcon', this.failIcon)
    }
  }
}
</script>

<style scoped>
 img{
   clip-path: circle(25px at center);
 }
 .full {
   clip-path: circle(35px at center);
 }
</style>
