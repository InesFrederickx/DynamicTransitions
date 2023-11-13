<template>
    <div id="preloader" v-if="isLoading">
    <div class="loading-ball"></div>
  </div>
    <div id="app">
        <header class="app-header">
            Mitosis
        </header>
        <div v-for="(stage, index) in evolutionStages" :key="stage.id" class="evolution-stage" :id="'section' + index">
        <div>
          <p>{{ stage.description }}</p>
          <img :src="stage.image" :alt="`Stage ${stage.id}`" @mouseenter="hoverStart" @mouseleave="hoverEnd"/>
        </div>
    </div>
    </div>
</template>

  
<script>
  import { gsap } from 'gsap';
  /*import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import SplitType from 'split-type'

  const ourText = new SplitType('p.our-text', { types: 'chars' })
  const chars = ourText.chars*/

  /*gsap.registerPlugin(ScrollTrigger);*/

  export default {
    name: 'App',
    data() {
      return {
        isLoading: true,
        evolutionStages: [
          { id: 1, image: 'public/img/prophase.png', description: 'Prophase, chromatin into chromosomes, the nuclear envelope break down, chromosomes attach to spindle fibres by their centromeres.' },
          { id: 2, image: 'public/img/metaphase.png', description: 'Metaphase, chromosomes line up along the metaphase plate (centre of the cell).' },
          { id: 3, image: 'public/img/anaphase.png', description: 'Anaphase, sister chromatids are pulled to opposite poles of the cell.' },
          { id: 4, image: 'public/img/telophase.png', description: 'Telophase, nuclear envelope reforms, chromosomes unfold into chromatin, cytokinesis can begin.' },
        ],
      };
    },
    mounted() {
    this.animatePreloader();
    /*this.animateHeader();*/

    /*gsap.utils.toArray('.evolution-stage').forEach((section, index) => {
    ScrollTrigger.create({
      trigger: section,
      start: 'top top',
      end: 'bottom bottom',
      pin: true,
      scrub: 1,
      snap: 1 / (this.evolutionStages.length - 1)
    });
  })*/
  },

  methods: {
    hoverStart(event) {
    gsap.to(event.target, {
      scale: 1.1, // Scales the image up to 110%
      ease: 'power1.inOut',
      duration: 0.3
    });
    },
    hoverEnd(event) {
        gsap.to(event.target, {
        scale: 1, // Scale back to normal
        ease: 'power1.inOut',
        duration: 0.3
        });
    },

  animatePreloader() {
    let tl = gsap.timeline({
      repeat: 6,
      yoyo: true,
      onComplete: () => {
        gsap.to('#preloader', {
          opacity: 0,
          duration: 0.5,
          onComplete: () => {
            this.isLoading = false;
          }
        });
      }
    });

    tl.to('.loading-ball', {
      y: -100,
      duration: 0.3,
      ease: 'power1.inOut'
    });

    


    /*animateHeader() {
    gsap.fromTo(
      '.app-header',
      { y: -100, opacity: 0 },
      { y: 0, opacity: 1, duration: 2, ease: 'power4.out' }
    );
    },
    }*/

  /*handleScrollEnd(index) {
    if (index < this.evolutionStages.length - 1) {
      // Smoothly scroll to the next section
      gsap.to(window, { scrollTo: { y: "#section" + (index + 1), autoKill: false }, duration: 1 });
    }
  };
  handleScrollStart(index) {
    if (index > 0) {
      // Smoothly scroll to the previous section
      gsap.to(window, { scrollTo: { y: "#section" + (index - 1), autoKill: false }, duration: 1 });
    }
  }*/
    },
    }
  }
</script>
  
<style>
  #preloader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: white;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  transition: opacity 1s ease-out;
}

.loading-ball {
  width: 20px;
  height: 20px;
  background-color: #F9A602;
  border-radius: 50%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}


#app {
  background-color: #e8e7e3;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 12px;
}

.app-header {
  text-align: center;
  font-size: 2em;
  font-weight: bold;
  padding: 20px;
  color: #333;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
}

.evolution-stage {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  padding: 20px;
  box-sizing: border-box;
}

.evolution-stage div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.evolution-stage img {
  width: 30%;
  max-width: 600px;
  
}

.evolution-stage p {
  width: 50%;
  max-width: 600px;
  font-size: 1.2em;
  color: black;
}
</style>