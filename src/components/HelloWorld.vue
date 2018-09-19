<template>
  <div>
    <div id="background-wrapper">
      <vue-flux
        :options="fluxOptions"
        :images="fluxImages"
        :transitions="fluxTransitions"
        :captions="fluxCaptions"
        ref="slider">
      </vue-flux>
      
      <div id="controller-wrapper">
        <button @click="start()">START</button>
        <button @click="$refs.slider.showImage('next')">NEXT</button>
      </div>
    </div>

    <div id="caption-wrapper">
      <div id="caption">
        {{currentCaption()}}
      </div>
    </div>
  </div>
</template>

<script>
import { VueFlux, Transitions, FluxCaption } from 'vue-flux';
import Vue from 'vue';

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
      return this.$refs.slider.captions[this.currentImage];
    },
    fluxOptions: {
      autoplay: false,
      fullscreen: true,
      bindKeys: true,
      delay: 3000,
    },
    fluxImages: [
      './static/background/yharnam001.jpg',
      './static/background/yharnam002.jpg',
      './static/background/yharnam003.png',
    ],
    fluxTransitions: {
      transitionFade: Transitions.transitionFade
    },
    fluxCaptions: [
      'bloodbornebloodbornebloodbornebloodbornebloodbornebloodborne',
      '이런 세상에, 무엇이었나? 사냥 때문인가, 피 때문인가, 아니면 끔찍한 악몽 때문인가?',
      '이런 세상에, 무엇이었나? 사냥 때문인가, 피 때문인가, 아니면 끔찍한 악몽 때문인가?'
    ]
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
  bottom: 50px;
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
  position: relative;
  left: -50%;
}
</style>
