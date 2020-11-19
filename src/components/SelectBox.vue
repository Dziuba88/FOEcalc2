<template lang="pug">
  .selectbox
    .selectbox--toggle(@click="selectboxToggle" ref="selectboxToggle")
      .selectbox--toggle__content
        span.label: slot(name='label')
        span.value: slot(name='value')
    nav.selectbox--menu
      vue-simple-scrollbar(scrollbarColor="rgba(218, 168, 91, 0.95)")
        slot(name='menu_items') Empty Dropdown Menu
</template>
<script>
import VueSimpleScrollbar from 'vue-simple-scrollbar'

export default {
  name: 'SelectBox',
  props: {
    placeholder: {
      type: String,
      default: '',
    },
    text: {
      type: String,
      default: 'Dropdown',
    },
    options: [],
  },
  components: {
    VueSimpleScrollbar,
  },
  methods: {
    selectboxToggle: function (event) {
      event.target.closest('.selectbox').classList.toggle('open')
    },

    documentClick(e) {
      let el = this.$refs.selectboxToggle
      let target = e.target
      if (el !== target && !el.contains(target)) {
        el.closest('.selectbox').classList.remove('open')
      }
    },
  },
  created() {
    document.addEventListener('click', this.documentClick)
  },
  destroyed() {
    document.removeEventListener('click', this.documentClick)
  },
}
</script>
<style>
@import '~vue-simple-scrollbar/dist/vue-simple-scrollbar.css';

.selectbox--menu {
  max-height: 200px;
  overflow: auto;
}
.selectbox--menu .v-ss {
  height: 200px;
}

.selectbox--menu .ss-scroll {
  width: 4px;
  margin-left: -1px;
  border-radius: 0;
  opacity: 1 !important;
}
.selectbox--menu .ss-content {
  padding: 0;
}
</style>
