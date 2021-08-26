<template>
  <div class="waypoint-dom">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      xmlns:bx="https://boxy-svg.com"
      viewBox="0 0 40 60"
    >
      <defs>
        <linearGradient
          gradientUnits="userSpaceOnUse"
          x1="60"
          y1="60"
          x2="110"
          y2="110"
          id="gradient-0"
        >
          <stop offset="0" class="start-color" />
          <stop offset="100%" class="end-color" />
        </linearGradient>
        <linearGradient
          gradientUnits="userSpaceOnUse"
          x1="12"
          y1="12"
          x2="27"
          y2="27"
          id="gradient-1"
        >
          <stop offset="0" class="start-color-2" />
          <stop offset="100%" class="end-color-2" />
        </linearGradient>
      </defs>
      <g
        transform="matrix(0.97665, 0, 0, 1, -77.199661, -61.783298)"
        class="marker-base"
        style="fill: url('#gradient-0')"
      >
        <path
          d="M 89.449 64.616 C 96.375 60.633 104.198 61.236 110.345 64.543 C 113.133 66.043 118.64 72.17 118.782 81.192 C 118.926 90.353 112.448 97.404 109.161 102.485 C 106.318 106.88 101.916 118.128 100 118.095 C 98.391 118.067 93.124 106.064 90.455 102.339 C 88.068 99.008 81.227 91.323 80.804 82.391 C 80.474 75.438 83.064 68.369 89.449 64.616 Z"
          style="fill: url('#gradient-0')"
        />
      </g>
      <circle
        style="fill: url('#gradient-1')"
        cx="20.91"
        cy="19.774"
        r="11.664"
        transform="matrix(0.97665, 0, 0, 1, -0.000005, -0.158351)"
        class="marker-circle"
      />
    </svg>
    <div class="waypoint-str-container">
      <div class="waypoint-str">{{ input }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WaypointSVG",
  props: {
    input: Number,
  },
};
</script>

<style scoped>
.waypoint-str-container {
  width: 100%;
  text-align: center;
}

.waypoint-str {
  color: white;
}

.waypoint-dom > svg {
  display: flex;
  width: 100px;
  justify-content: center;
  align-items: center;
}

.waypoint-dom:hover {
  animation: get-big 0.5s linear both;
}

@keyframes get-big {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.1);
  }
}

.start-color {
  stop-color: red;
}
.end-color {
  stop-color: blue;
}
.start-color-2 {
  stop-color: rgba(255, 255, 255, 0.856);
}
.end-color-2 {
  stop-color: rgb(0, 0, 0);
}
</style>
