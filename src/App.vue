<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="text-center">
          <h1>Tell a Joke with Microsoft Azure</h1>
          <br/>
        </div>
        <h3>
          Demo usage of serverless functions on Microsoft Azure. <Br />
        </h3>
        <p>
          This demo application converts a joke received from a remote cloud function and converts it to speech using another cloud function and plays it on the user's computer. Turn on your speakers !
        </p>
        <br />
        <h3>
          Workflow
        </h3>
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
          <small>
              This application is tested on Firefox 66.0.5 and Google Chrome 74.0.3729.157
          </small>
      </div>
    </div>
    <hr />
    <JokeComponent></JokeComponent>
    <br />
    <hr />
    <small>
      Developed by Alvin Loh. Follow me on <a href="http://twitter.com/AlvinLoh19">Twitter</a>
      <Br />
      Jokes library created by Elijah Manor. Follow <a href="https://twitter.com/elijahmanor">him</a> on Twitter
      <br />
      Tutorial to follow
    </small>
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
