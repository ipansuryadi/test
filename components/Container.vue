<template>
  <div class="container" ref="scroll">
    <slot />
  </div>
</template>
<script>
const jump = 200;
export default {
  name: "Container",
  props: ["position"],
  watch: {
    position(val) {
      this.$refs.scroll.scrollTo(val, 0);
    }
  },
  methods: {
    detectMouseWheel() {
      var item = this.$refs.scroll;
      window.addEventListener("wheel", function(e) {
        if (e.deltaY > 0) item.scrollLeft += jump;
        else item.scrollLeft -= jump;
        localStorage.setItem("scrollPosition", item.scrollLeft);
      });
    }
  },
  mounted() {
    this.detectMouseWheel();
  }
};
</script>