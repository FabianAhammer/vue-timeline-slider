<template>
  <div class="page-pwa">
    <div class="header-pwa">Ordinary Header</div>
    <div class="timeline-container">
      <div class="timeline-header">My Timeline</div>
      <div class="timeline-container-inner">
        <div class="timeline-container-inner-bg">
          <div class="timeline-head-container">
            <div class="bwd-ico">
              <button v-on:click="moveslider(true)" class="ico-btn">
                &lt;
              </button>
            </div>
            <div class="fwd-ico">
              <button v-on:click="moveslider(false)" class="ico-btn">></button>
            </div>
          </div>
          <div
            ref="timeline"
            v-on:mousedown="mousedown"
            v-on:mousemove="mousemove"
            v-on:mouseleave="isDown = false"
            v-on:mouseup="
              isDown = false;
              beginMomentumTracking;
            "
            class="timeline-content"
          >
            <div
              class="timeline-item-container"
              v-for="(number, index) in Array(50)"
              :key="index"
            >
              <Waypoint v-bind:input="index"></Waypoint>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="js">
import Waypoint from "./Waypoint.vue";
export default {
  name: "SS",
  components: {
    Waypoint,
  },
  data() {
    return {
      isDown: false,
      slider: null,
      velX: 0,
      scrollLeft: 0,
      startX: 0,
      momentumID: null,
    };
  },
  methods: {
    moveslider(positiveBool){
      if(positiveBool === true){

        this.$refs.timeline.scrollLeft -= 260;
      }
      else if(positiveBool === false){
        this.$refs.timeline.scrollLeft += 260;
      }
    },
    mousedown(e) {
      this.isDown = true;
      this.startX = e.pageX - this.$refs.timeline.offsetLeft;
      this.scrollLeft = this.$refs.timeline.scrollLeft;
      this.cancelMomentumTracking();
    },
    mousemove(e) {
      if (!this.isDown) return;
      const slider = this.$refs.timeline;
      e.preventDefault();
      const x = e.pageX - slider.offsetLeft;
      const walk = (x - this.startX) * 3;
      // Store the previous scroll position
      var prevScrollLeft = slider.scrollLeft;
      slider.scrollLeft = this.scrollLeft - walk;
      // Compare change in position to work out drag speed
      this.velX = slider.scrollLeft - prevScrollLeft;
    },
    beginMomentumTracking() {
      this.momentumID = requestAnimationFrame(this.momentumLoop);
    },
    cancelMomentumTracking() {
      cancelAnimationFrame(this.momentumID);
    },
    momentumLoop() {
      this.$refs.timeline.scrollLeft += this.velX;
      this.velX *= 0.8;
      if (Math.abs(this.velX) > 0.8) {
        this.momentumID = requestAnimationFrame(this.momentumLoop);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.timeline-item-container {
  display: flex;
  padding: 0px 80px;
}
.timeline-items {
  width: 14px;
  height: 70%;
  margin-top: 50px;
  background-color: red;
  padding: 0px 10px 0px 10px;
  margin: 0px 80px 0px 80px;
}
.timeline-items:hover {
  animation: larger-bg-x3 1s linear both;
}
@keyframes larger-bg-x3 {
  0% {
    transform: scale(1);
  }

  100% {
    transform: scale(1.3);
  }
}

.timeline-item-container:hover > .message-on-info {
  animation: fade-in 1s linear both;
}
@keyframes larger-bg-x3 {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

.timeline-container-inner-bg {
  height: 100%;
  width: 100%;
  background: rgba(146, 146, 146, 0.219);
  padding: 11px;
  border: rgba(85, 85, 85, 0.356) solid 1px;
  border-radius: 15px;
}

.timeline-content {
  padding-top: 26px;
  height: 90%;
  overflow-x: scroll;
  width: 68vw;
  display: flex;
  flex: none;
  flex-direction: hidden;
  overflow-x: hidden;
  overflow-y: hidden;
}
.ico-btn {
  font-weight: bold;
  line-height: 1;
  color: white;
  font-size: 1.4em;
  border-radius: 1em;
  border: 0.1px solid white;
  width: 28px;
  height: 28px;
}
.timeline-header {
  margin-bottom: 25px;
  color: white;
  width: 100%;
  text-align: center;
  font-size: 1.2em;
}
.fwd-ico {
  margin-right: 10px;
}
.bwd-ico {
  margin-left: 10px;
}

.timeline-head-container {
  display: flex;
  justify-content: space-between;
  height: 10%;
  width: 100%;
  align-items: center;
}
.timeline-container-inner {
  margin-left: 15%;
  margin-right: 15%;
  background: linear-gradient(
    to bottom,
    transparent 56%,
    white 56%,
    white 58%,
    transparent 58%
  );
  width: 70%;
  height: 100%;
}

.timeline-container {
  margin-top: 10%;
  width: 100%;
  height: 30vh;
}
.page-pwa {
  height: 100vh;
  width: 100vw;
  background-color: rgb(43, 41, 41);
}

.header-pwa {
  height: 10vh;
  width: 100%;
  display: flex;
  color: white;
  font-size: 5em;
  text-align: center;
  justify-content: center;
  font-family: "Arial";
  -webkit-animation: focus-in-expand 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94)
    both;
  animation: focus-in-expand 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) both;
}

@-webkit-keyframes focus-in-expand {
  0% {
    letter-spacing: -0.5em;
    -webkit-filter: blur(12px);
    filter: blur(12px);
    opacity: 0;
  }
  100% {
    -webkit-filter: blur(0);
    filter: blur(0);
    opacity: 1;
  }
}
@keyframes focus-in-expand {
  0% {
    letter-spacing: -0.5em;
    -webkit-filter: blur(12px);
    filter: blur(12px);
    opacity: 0;
  }
  100% {
    -webkit-filter: blur(0);
    filter: blur(0);
    opacity: 1;
  }
}
</style>
