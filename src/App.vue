<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="text-center">
          <h1>Azure Tell a Joke</h1>
          <br/>
        </div>
        <h3>
          Demo usage of serverless functions on Azure. <Br />
        </h3>
        <br />
        <h5>
          Get a Random Joke
        </h5>
        <p>
          When you press the "Tell a Joke" button, the Vue application calls the first Azure function to get a random joke.
        </p>
        <h5>
          Text to Speech Conversion
        </h5>
        <p>
          Upon fetch completion, the application calls another Azure function to convert the received text to speech.
        </p>
        <h5>
          Playing the generated sound file
        </h5>
        <p>
          The application then pushes the generated sound file to the audio control to be played.
        </p>
      </div>
    </div>
    <hr />
    <JokeComponent></JokeComponent>
  </div>
</template>

<script>
import JokeComponent from './components/JokeComponent.vue'

export default {
  name: "app",
  components: {
    JokeComponent
  }
};
</script>

<style>
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  text-decoration:underline;
}
</style>
