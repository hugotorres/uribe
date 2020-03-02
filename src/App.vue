<template>
  <div id="app">
    <meta data-vue-meta="custom" charset="utf-8" />
    <div class="titulo text-center">
      <h1>Uribe Quotes</h1>
    </div>
    <div id="fullpage" v-if="isLoaded" class="color6">
      <div v-for="showerThought in showerThoughts" :key="showerThought.id" class="section wrapper">
        <div class="logo sidebar" @click="update">
          <img src="./assets/uribe.png" alt="Uribe Velez" height="120px" />
        </div>
        <div class="content">
          <div class="quote">
            <div class="quote-symbol left">“</div>

            {{ showerThought}}
            <div class="quote-symbol right">“</div>
          </div>
          <!-- <div class="details">
              <div class="details-author">Author: {{ showerThought.data.author }}</div>
              <div class="details-stats">{{ showerThought.data.ups }} Upvote | {{ showerThought.data.num_comments }} Comments</div>
          </div>-->
        </div>
        <div class="mobile-img" @click="update">
          <img src="./assets/uribe.png" alt="Uribe Velez" height="120px" />
        </div>
      </div>
    </div>
    <div v-else>
      <loading-spinner />
    </div>
  </div>
</template>

<script>
import LoadingSpinner from "./components/LoadingSpinner.vue";
export default {
  name: "App",
  components: {
    LoadingSpinner
  },
  created() {
    //fetch("https://www.reddit.com/r/showerthoughts.json?limit=20")
    fetch("https://old-art-46ef.andrestorres.workers.dev/")
      .then(response => response.json())
      .then(data => {
        this.showerThoughts = data;
        this.isLoaded = true;
      });
  },
  methods: {
    getColor: function() {
      const numero = Math.floor(Math.random() * 5);
      console.log(numero);
      const color = this.colors[numero];
      console.log(color);
      return color;
    },
    update: function() {
      this.fetch();
      const color = this.getColor();
      document.getElementById("fullpage").className = color;
      console.log(color);
    },
    fetch: function() {
      fetch("https://old-art-46ef.andrestorres.workers.dev/")
        .then(response => response.json())
        .then(data => {
          this.showerThoughts = data;
          this.isLoaded = true;
        });
    }
  },
  data() {
    return {
      isLoaded: false,
      showerThoughts: [],
      colors: ["color1", "color2", "color3", "color4", "color5", "color6"]
    };
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Sriracha&display=swap");
#app {
  font-family: sans-serif;
  color: #2d3748;
}
#fullpage {
  height: 100vh;
}
body {
  margin: 0;
  padding: 0;
}
h3 {
  margin: 0;
}
.color1 {
  background-color: rgb(41, 162, 136);
}
.color2 {
  background-color: #231651;
}
.color3 {
  background: #4dccbd;
}
.color4 {
  background: #2374ab;
}
.color5 {
  background-color: #ff8484;
}
.color6 {
  background-color: rgb(245, 63, 63);
}

.titulo h1 {
  padding: 0px 20px;
}
.section {
  text-align: center;
}
.logo {
  cursor: pointer;
}
.logo img {
  height: 80vh;
  position: absolute;
  bottom: 0px;
}
.quote-symbol {
  font-size: 64px;
  line-height: 0.5;
  margin-top: 50px;
  color: white;
}
.quote-symbol.left {
  text-align: left;
}
.quote-symbol.right {
  text-align: right;
}

.quote {
  text-decoration: none;
  font-family: "Sriracha", cursive;
  color: #ffffff;
  font-size: 32px;
  line-height: 1.5;
  padding: 5px 15px;

  background: #fdfdfd1c;
  border: radius;
  border-radius: 31px;
  -webkit-box-shadow: #5b5b5b52 13px 14px 19px 8px;
  box-shadow: #5b5b5b52 13px 14px 19px 8px;
}
.quote hover {
  color: #edf2f7;
}
.details-stats {
  margin-top: 4px;
}
.logo.sidebar:before {
  content: "";
  height: 80vh;
  background: black;
  bottom: 0;
  position: absolute;
  background: url(/img/uribe.3a354e49.png);
  background-size: contain;
  background-repeat: no-repeat;
  /* transform: skew(19deg, -1deg); */
  filter: blur(15px);
}
.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
  position: relative;

  padding: 15px 10%;
}

.wrapper {
  display: grid;
  grid-gap: 0px;
  grid-template-columns: 33vw 66vw;
  grid-template-areas: "sidebar content ";
}
.mobile-img {
  display: none;
}
@media (max-width: 500px) {
  .mobile-img {
    display: block;

  }
      .mobile-img img {
      height: 35vh;
    }
  .logo img {
    height: 40vh;
    position: absolute;
    bottom: 0px;
    display: none;
  }
  .wrapper {
    display: grid;
    grid-gap: 0px;
    grid-template-columns: 33vw 66vw;
    grid-template-areas: "sidebar sidebar" "content content";
  }
  .logo.sidebar:before {
    content: "";
    height: 250px;
    background: black;
    bottom: 0;
    position: absolute;
    background: none;
  }
  .quote {
    font-size: 18px;
    background: #fdfdfd1c;
    border: radius;
    border-radius: 31px;
    -webkit-box-shadow: #5b5b5b52 13px 14px 19px 8px;
    box-shadow: #5b5b5b52 13px 14px 19px 8px;
  }
}
* {
  transition: all 0.3s ease-in;
}
</style>