<template>
  <speedkit-layer class="page-info-layer">
    <div>
      <p v-font="$getFont('Raleway', 400, 'normal')">
        Sorry, but you will have a limited user experience due to a…
      </p>
      <ul v-font="$getFont('Raleway', 700, 'normal')">
        <li id="nuxt-speedkit-message-nojs">
          disabled javascript
        </li>
        <li id="nuxt-speedkit-message-unsupported-browser">
          outdated browser
        </li>
        <li id="nuxt-speedkit-message-reduced-bandwidth">
          reduced-bandwidth
        </li>
        <li id="nuxt-speedkit-message-weak-hardware">
          weak hardware
        </li>
      </ul>
      <div class="buttons">
        <base-button id="nuxt-speedkit-button-init-nojs">
          <label for="nuxt-speedkit-layer-close">
            OK
          </label>
        </base-button>
        <base-button id="nuxt-speedkit-button-init-font" onclick="window.__NUXT_SPEEDKIT_FONT_INIT__ = true;">
          <label for="nuxt-speedkit-layer-close">
            No
          </label>
        </base-button>
        <base-button id="nuxt-speedkit-button-init-app" label="Yes" onclick="window.__NUXT_SPEEDKIT_AUTO_INIT__ = true;" />
      </div>
    </div>
  </speedkit-layer>
</template>

<script>

import SpeedkitLayer from 'nuxt-speedkit/components/SpeedkitLayer';
import { getStyleDescription } from 'nuxt-speedkit/utils/description';
import BaseButton from '@/components/atoms/BaseButton';

export default {
  components: {
    BaseButton,
    SpeedkitLayer
  },
  data () {
    return {
      hydrate: false
    };
  },
  head () {
    return this.$speedkit.head({
      noscript: [
        getStyleDescription('.page-info-layer > div { animation-delay: initial !important; }', true)
      ],
      __dangerouslyDisableSanitizers: [
        'noscript'
      ]
    });
  }
};
</script>

<style lang="postcss" scoped>
.page-info-layer {
  & >>> #nuxt-speedkit-layer-content {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1000;
    width: 100%;
    height: 100%;
    background-color: rgb(0 0 0 / 25%);
    opacity: 0;
    animation-name: fade-in;
    animation-duration: 0.2s;
    animation-delay: 3s;
    backdrop-filter: blur(calc(7 / 16 * 1em));
    animation-fill-mode: forwards;

    & > div {
      padding: 10px;
      color: #fff;
      text-align: center;
      background-color: rgb(0 0 0 / 60%);
      box-shadow: 0 0 calc(10 / 16 * 1em) rgb(0 0 0 / 60%);
      transform: translateY(-100%);
      animation-name: fall-down;
      animation-duration: 0.2s;
      animation-delay: 0.5s;
      animation-fill-mode: forwards;
    }
  }

  &.nuxt-speedkit-layer-visible {
    & >>> #nuxt-speedkit-layer-content {
      animation-delay: initial;
    }
  }

  & .buttons {
    margin: calc(10 / 16 * 1em) 0;

    & > * {
      margin: 0 calc(5 / 16 * 1em);
    }
  }
}

ul {
  padding: 0;
  margin: 0;

  & > li {
    display: none;
  }
}

@keyframes fade-in {
  100% {
    opacity: 1;
  }
}

@keyframes fall-down {
  100% {
    transform: translateY(0%);
  }
}

</style>
