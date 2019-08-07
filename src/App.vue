<template>
  <div id="app">
    <header>
      <h1>
        <img src="assets/pokeball.png" width="5%" height="5%" style="vertical-align: middle;" /> PokeMan
      </h1>
    </header>
    <main>
      <div class="row">
        <div class="column-left" style="background-color:#aaa;opacity: 1;">
          <ul>
            <router-link
              v-for="pokemon in pokemons"
              active-class="is-active"
              v-bind:key="pokemon.name"
              class="link"
              :to="{ name: 'PokemonDetail', params: { name: pokemon.name } }"
            >
              <li>{{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}</li>
            </router-link>
          </ul>
        </div>
        <div class="column-right" style="background-color:#bbb;opacity: 0.5;">
          <div class="content">
            <router-view></router-view>
          </div>
        </div>
      </div>

      <div id="pocket">
        <a href="#pocketmonster" @click="setToTop">
        <img src="assets/pocket.png" />
        </a>
      </div>
    </main>
    <div class="modal" id="pocketmonster">
      <div class="modal-container">
        <h2><img src="assets/pocketicon.png" style="position: relative; vertical-align: middle;"/>
        Your Pokemon Pocket</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum ac iaculis est. Proin a nisl sit amet turpis facilisis euismod. Praesent sit amet nisl ornare, volutpat orci at, pretium ipsum. Sed sed ante a ex vulputate iaculis sed et mauris. Suspendisse potenti. In hac habitasse platea dictumst.</p>
        <a href="#modal-close">Close</a>
      </div>
    </div>
  </div>
</template>
<style>
body {
  background-color: #272727;
  background-image: url("assets/background.jpg");
  background-position: bottom right;
  background-repeat:no-repeat;
  background-attachment: fixed;
},
@keyframes bounce {
 0%, 20%, 60%, 100% {
   -webkit-transform: translateY(0);
   transform: translateY(0);
 }
 40% {
   -webkit-transform: translateY(-20px);
   transform: translateY(-20px);
 }
 80% {
   -webkit-transform: translateY(-10px);
   transform: translateY(-10px);
 }
},
@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
* {
  box-sizing: border-box;
}

/* Create two equal columns that floats next to each other */
.column {
  float: left;
  width: 20%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}
.column-left {
  float: left;
  width: 20%;
  padding: 10px;
  height: 50%; /* Should be removed. Only for demonstration */
  overflow: scroll;
}
.column-right {
  opacity: 0.5;
  float: left;
  width: 80%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}

.column-sprites {
  float: left;
  width: 25%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}

#pocket img {
  position: fixed;
  right: 0px;
  bottom: 0%;
}

.pocket-bounces {
  animation: bounce 1s infinite;
}
#pocket-shake img {
  position: fixed;
  right: 0px;
  bottom: 0%;
  animation: shake 1s infinite;
  -webkit-animation: shake 1s infinite;
  -moz-animation: shake 1s infinite;
  -o-animation: shake 1s infinite;
}
/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
p {
  margin-top: 0;
}
.modal-container {
  position: fixed;
  background-color: #fff;
  width: 70%;
  max-width: 80%;
  height: 80%;
  left: 50%;
  padding: 20px;
  border-radius: 5px;
  -webkit-transform: translate(-50%, -200%);
  -ms-transform: translate(-50%, -200%);
  transform: translate(-50%, -200%);
  -webkit-transition: -webkit-transform 200ms ease-out;
  transition: transform 200ms ease-out;
}
.modal:before {
  content: "";
  position: fixed;
  display: none;
  background-color: rgba(0, 0, 0, 0.8);
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}
.modal:target:before {
  display: block;
}
.modal:target .modal-container {
  top: 5%;
  -webkit-transform: translate(-50%, 0%);
  -ms-transform: translate(-50%, 0%);
  transform: translate(-50%, 0%);
}
#modal-close {

}
</style>
<script>
import axios from "axios";
export default {
  data() {
    return {
      pokemons: null,
      endpoint:
        "https://pokeapi.co/api/v2/pokemon?offset=0&limit=10000000000000000"
    };
  },

  created() {
    this.getAllPosts();
  },

  methods: {
    getAllPosts() {
      this.pokemons =  null
      axios
        .get(this.endpoint)
        .then(response => {
          this.pokemons = response.data.results;
        })
        .catch(error => {
          console.log("-----error-------");
          console.log(error);
        });
    },
    setToTop() {
      // alert('tes')
      setTimeout(function(){
      document.body.scrollTop = 0; // For Safari
      document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
      }, 100);
    }
  }
};
</script>
