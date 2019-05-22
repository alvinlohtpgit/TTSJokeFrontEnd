<template>
  <div class="row">
    <div class="col-md-12">
      <div class="jokedisplaypanel">
        <h4>Random Joke</h4>
        <p>{{ jokedisplay }}</p>
        <br />
        <b-button size="lg" @click="randomjokeclick">Tell a Joke</b-button>
        <audio ref="audioplay" :src="musicSrc" preload="auto"></audio>
      </div>
    </div>
  </div>
</template>

<script>
import querystring from "querystring";

export default {
  name: "JokeComponent",
  data() {
    return {
      jokedisplay: "(Please press the button below to retrieve a random joke)",
      musicSrc:
        "https://ttsjokestorage.blob.core.windows.net/ttsjoketemp/TTSOutput.wav"
    };
  },
  methods: {
    randomjokeclick() {
      this.$http
        .get(
          "https://ttsjokefa.azurewebsites.net/api/GetJoke?code=owJIuVXd4FUar1QvqxIdMvOY/w5QMWCNqXsKdYgKU6B9byvhOEC18A=="
        )
        .then(response => {
          // Update the jokedisplay
          // this.jokedisplay = response.data;
          console.log("Joke received : " + response.data);
          // Next we call the convert tts function
          this.$http
            .post(
              "https://ttsjokefa.azurewebsites.net/api/ConvertTTS?code=FghVeXjL5R/4P1Sa0P1yWqc6suiva90yBBD8/bQBADANrymxeiwErA==",
              querystring.stringify({ saythis: "Hello World 5" }),
              {
                headers: { "Content-Type": "application/x-www-form-urlencoded" }
              }
            )
            .then(responsetts => {
              console.log("File generated");
              // The file is generated
              this.jokedisplay = response.data;

              /*

              var delay = ( function() {
    var timer = 0;
    return function(callback, ms) {
        clearTimeout (timer);
        timer = setTimeout(callback, ms);
    };
})();
Usage:

delay(function(){
    // do stuff
}, 5000 ); // end delay


               */

              this.$refs.audioplay.play();
            })
            .catch(error => { console.log('Error Post ' + error) });
        });
    }
  },
  mounted() {
    //this.$refs.audioplay.play();
  }
};
</script>

<style scoped>
.jokepanel {
  margin-top: 30px;
}

.jokedisplaypanel {
  padding-top: 35px;
  text-align: center;
}
</style>
