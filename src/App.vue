<template>
  <div id="app">
    <header>
      <h1><img src="assets/pokeball.png" width="5%" height="5%" style="vertical-align: middle;"/> PokeMan</h1>
    </header>
    <main>

<div class="row">
  <div class="column-left" style="background-color:#aaa;">
 <ul>
    <router-link
        v-for="pokemon in pokemons"
        active-class="is-active"
        v-bind:key="pokemon.name"
        class="link"
        :to="{ name: 'PokemonDetail', params: { name: pokemon.name } }">
      <li>{{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}</li>
    </router-link>
    </ul>
  </div>
  <div class="column-right" style="background-color:#bbb;">
   <div class="content">
        <router-view></router-view>
      </div>
  </div>
</div>

<div id="pocket">
    <img src="assets/pocket.png" />
</div>

    </main>
  </div>
</template>
<style>
@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
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
</style>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      pokemons: null,
      endpoint: 'https://pokeapi.co/api/v2/pokemon?offset=0&limit=10000000000000000',
    }
  },

  created() {
    this.getAllPosts();
  },

  methods: {
    getAllPosts() {
      axios.get(this.endpoint)
        .then(response => {
          this.pokemons = response.data.results;
        })
        .catch(error => {
          console.log('-----error-------');
          console.log(error);
        })
    }
  }
}
</script>
