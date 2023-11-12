<template>
    <div id="app">
      <div v-for="stage in evolutionStages" :key="stage.id" class="evolution-stage">
        <div>
          <p>{{ stage.description }}</p>
          <img :src="stage.image" :alt="`Stage ${stage.id}`" />
        </div>
      </div>
    </div>
</template>

  
  <script>
  export default {
    name: 'App',
    data() {
      return {
        evolutionStages: [
          { id: 1, image: 'public/img/giraffe.jpg', description: 'Description for Stage 1' },
          { id: 2, image: 'public/img/giraffe.jpg', description: 'Description for Stage 2' },
          { id: 3, image: 'public/img/giraffe.jpg', description: 'Description for Stage 3' },
          { id: 4, image: 'public/img/giraffe.jpg', description: 'Description for Stage 4' },
          { id: 5, image: 'public/img/giraffe.jpg', description: 'Description for Stage 5' }
          
        ],
      };
    },
  };
  </script>
  
  <style>
#app {
  background-color: white;
}

.evolution-stage {
  display: flex;
  flex-direction: column; /* Stack each stage vertically */
  justify-content: center;
  align-items: center;
  height: 100vh; /* Full viewport height for each stage */
  padding: 20px;
  box-sizing: border-box; /* Include padding in height calculation */
}

.evolution-stage div {
  display: flex; /* Inner flex container */
  justify-content: space-between; /* Space out text and image */
  align-items: center;
  width: 100%; /* Full width of the stage */
}

.evolution-stage img {
  width: 50%;
  max-width: 600px;
  height: auto;
}

.evolution-stage p {
  width: 50%;
  max-width: 600px;
  font-size: 1.2em;
  color: black; /* Black text color */
}
</style>
