<template>
  <div class="row">
    <div class="col-md-12">
      <div class="jokedisplaypanel">
        <h4>Random Joke</h4>
        <p>{{ jokedisplay }}</p>
        <br />
        <b-button size="lg" @click="randomjokeclick">Tell a Joke</b-button>
        <audio ref="audioplay" :src="musicSrc" preload="none"></audio>
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
      musicSrc: ""
    };
  },
  methods: {
    randomjokeclick() {
      this.jokedisplay = "Contacting Azure Function .. please wait";
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
              querystring.stringify({ saythis: response.data }),
              {
                headers: { "Content-Type": "application/x-www-form-urlencoded" }
              }
            )
            .then(responsetts => {
              console.log("File generated - " + responsetts.data);
              // The file is generated
              this.jokedisplay = response.data;

              this.musicSrc = "https://ttsjokestorage.blob.core.windows.net/ttsjoketemp/" + responsetts.data;
              console.log("Setting audio source file to " + this.musicSrc);

              console.log("Wait a while for Azure storage to refresh");
              setTimeout(() => this.$refs.audioplay.play(), 3000);
            })
            .catch(error => { console.log('Error Post ' + error) });
        });
    }
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
