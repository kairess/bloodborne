<template>
  <div>
    <div id="background-wrapper">
      <vue-flux
        :options="fluxOptions"
        :images="fluxImages"
        :transitions="fluxTransitions"
        ref="slider">
      </vue-flux>
      
      <div id="controller-wrapper">
        <button @click="start()">START</button>
        <button @click="$refs.slider.showImage('next')">NEXT</button>
      </div>
    </div>

    <div id="caption-wrapper">
      <div id="caption">
        {{currentCaption().en}}<br/>
        {{currentCaption().ko}}
      </div>
    </div>
  </div>
</template>

<script>
import { VueFlux, Transitions, FluxCaption } from 'vue-flux';
import Vue from 'vue';
import scripts from '../../static/data.json';

export default {
  name: 'HelloWorld2',
  components: {
    VueFlux,
    FluxCaption
  },
  mounted() {
    this.$watch(() => this.$refs.slider.currentImage.index, (value) => { this.currentImage = value;});
  },
  methods: {
    start() {
      console.log('started!');
      this.$refs.slider.play();
    }
  },
  data: () => ({
    currentImage: -1,
    currentCaption() {
      if (this.currentImage < 0) {
        return '';
      }
      return this.captions[this.currentImage];
    },
    fluxOptions: {
      autoplay: false,
      fullscreen: true,
      bindKeys: true,
      delay: 3000,
    },
    fluxImages: scripts.images,
    fluxTransitions: {
      transitionFade: Transitions.transitionFade
    },
    captions: scripts.captions
  })
}
</script>

<style scoped>
#background-wrapper {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

#controller-wrapper {
  position: absolute;
  bottom: 30px;
  right: 50px;
  z-index: 999;
}

#caption-wrapper {
  position: absolute;
  left: 50%;
  bottom: 50px;
  z-index: 999;
  height: 50px;
}

#caption {
  text-align: center;
  position: relative;
  left: -50%;
}
</style>
