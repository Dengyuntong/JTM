<template>
  <div style="touch-action: none;">
    <div
      class="home"
      style="position:fixed;"
      :style="{ top: top + 'px', bottom: bottom }"
      id="right-nav"
      ref="moveBtn"
      @touchmove="touchmove($event)"
    >
      <div
        class="homeCon bg-color-red"
        :class="homeActive === true ? 'on' : ''"
        v-if="homeActive"
        @click="open"
      >
        <router-link
          :to="'/'"
          class="iconfont icon-shouye-xianxing"
        ></router-link>
        <router-link
          :to="'/cart'"
          class="iconfont icon-caigou-xianxing"
        ></router-link>
        <router-link 
          :to="'/user'" 
          class="iconfont icon-yonghu1"
        ></router-link>
      </div>
      <div @click="open" class="pictrueBox">
        <div class="pictrue">
          <img
            :src="
              homeActive === true
                ? require('../assets/images/close.gif')
                : require('../assets/images/open.gif')
            "
            class="image"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  name: "Home",
  props: {},
  data: function() {
    return {
      top: "",
      bottom: ""
    };
  },
  computed: mapGetters(["homeActive"]),
  methods: {
    touchmove(event) {
      let cha = event.targetTouches[0].clientY - this.$refs.moveBtn.offsetTop
      this.bottom = "auto";
      event.preventDefault();
      let top = this.$refs.moveBtn.offsetTop + cha
        if(top < 10) {
          top = 10
        } else if(top > document.body.offsetHeight - event.target.offsetHeight - document.body.offsetHeight * 0.10) {
          top = document.body.offsetHeight - event.target.offsetHeight - document.body.offsetHeight * 0.10
        }
      this.top = top;
    },
    open: function() {
      this.homeActive
        ? this.$store.commit("CLOSE_HOME")
        : this.$store.commit("OPEN_HOME");
    }
  },
  created() {
    this.bottom = "50px";
  }
};
</script>

<style scoped>
.pictrueBox {
  width: 1.3rem;
  height: 1.2rem;
}
</style>
