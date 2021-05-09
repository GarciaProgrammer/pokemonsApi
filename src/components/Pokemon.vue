<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ nome | nameUpper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>
        <div class="content">
          <button class="button" @click="mudarImage()">Mudar sprite</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created() {
    axios.get(this.url).then((date) => {
      this.pokemon.type = date.data.types[0].type.name;
      this.pokemon.front = date.data.sprites.front_default;
      this.pokemon.back = date.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    nome: String,
    url: String,
    num: Number,
  },
  filters: {
    nameUpper(valor) {
      return valor[0].toUpperCase() + valor.slice(1);
    },
  },
  methods: {
    mudarImage() {
      this.isFront = !this.isFront;
      this.isFront ? this.currentImg = this.pokemon.front : this.currentImg = this.pokemon.back;
    },
  },
};
</script>

<style>
#pokemon {
  margin-top: 10px;
}
</style>