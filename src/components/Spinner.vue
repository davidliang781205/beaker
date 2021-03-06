<template>
  <div class="s-spinner">
    <div class="s-bars" :size="size" :swap="swap">
      <svg
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        :class="spinnerClass"
        viewBox="0 0 28 40"
      >
        <path d="M0 0, l0 4, l0 -4" id="s-bar-y-path"></path>
        <rect
          width="4"
          height="40"
          x="0"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar"
          :class="swapMode"
        >
          <animate
            attributeName="opacity"
            values=".24; .08; .24"
            begin="0s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animate
            attributeName="height"
            values="40; 32; 40"
            begin="0s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animateTransform
            v-if="firefox"
            attributeName="transform"
            type="translate"
            values="0 0 ; 0 4; 0 0"
            begin="0s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animateTransform>
          <animateMotion begin="0s" dur="1.2s" repeatCount="indefinite">
            <mpath xlink:href="#s-bar-y-path"></mpath>
          </animateMotion>
        </rect>
        <rect
          width="4"
          height="40"
          x="12"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar"
          :class="swapMode"
        >
          <animate
            attributeName="opacity"
            values=".24; .24; .24"
            begin="0s"
            dur="0.4s"
          ></animate>
          <animate
            attributeName="opacity"
            values=".24; .08; .24"
            begin="0.4s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animate
            attributeName="height"
            values="40; 32; 40"
            begin="0.4s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animateTransform
            v-if="firefox"
            attributeName="transform"
            type="translate"
            values="0 0 ; 0 4; 0 0"
            begin="0.4s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animateTransform>
          <animateMotion begin="0.4s" dur="1.2s" repeatCount="indefinite">
            <mpath xlink:href="#s-bar-y-path"></mpath>
          </animateMotion>
        </rect>
        <rect
          width="4"
          height="40"
          x="24"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar"
          :class="swapMode"
        >
          <animate
            attributeName="opacity"
            values=".24; .24; .24"
            begin="0s"
            dur="0.8s"
          ></animate>
          <animate
            attributeName="opacity"
            values=".24; .08; .24"
            begin="0.8s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animate
            attributeName="height"
            values="40; 32; 40"
            begin="0.8s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animate>
          <animateTransform
            v-if="firefox"
            attributeName="transform"
            type="translate"
            values="0 0 ; 0 4; 0 0"
            begin="0.8s"
            dur="1.2s"
            repeatCount="indefinite"
          ></animateTransform>
          <animateMotion begin="0.8s" dur="1.2s" repeatCount="indefinite">
            <mpath xlink:href="#s-bar-y-path"></mpath>
          </animateMotion>
        </rect>
      </svg>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({
  name: "Spinner"
})
export default class Spinner extends Vue {
  private firefox: Boolean = false;

  @Prop({ default: "small" })
  size!: String;

  @Prop({ default: false })
  swap!: Boolean;

  get spinnerClass() {
    return `s-spinner--${this.size}`;
  }

  get swapMode() {
    if (this.swap === true) {
      return "s-spinner--modeswap";
    }
  }

  mounted() {
    if (navigator.userAgent.indexOf("Firefox") != -1) {
      this.firefox = true;
    }
  }
}
</script>

<style lang="less">
@import (reference) "./../styles/Imports";

.s-spinner {
  width: 100%;
  height: 100%;
  .padding();
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;

  svg,
  path,
  rect {
    transform-origin: top;
  }
}

.s-spinner--tiny {
  height: 14px;
  width: 9px;
}

.s-spinner--small {
  height: 40px;
  width: 28px;
}

.s-spinner--large {
  height: 80px;
  width: 56px;
}

.s-spinner__bar {
  fill: @dark-2;

  &.s-spinner--modeswap {
    fill: @light-2;
  }
}

.night,
.night-theme {
  .s-spinner__bar {
    fill: @light-2;

    &.s-spinner--modeswap {
      fill: @dark-2;
    }
  }
}
</style>
