<template>
  <div class="poke">
    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentImg"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ upper(name) }}</p>
            <p class="subtitle is-6">{{pokemon.type}}</p>
          </div>
        </div>
            <button class="button is-primary is-hovered" @click="invertIMG">Inverter imagem</button>

        <div class="content">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    num: Number,
    name: String,
    url: String,
  },
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg=this.pokemon.front
    });
  },
  data() {
    return {
      currentImg:'',
      isFront:true,
      pokemon: {
          type:'',
          front:'',
          back:''
      },
    };
  },
  methods: {
    upper: function (value) {
      let formated = value[0].toUpperCase() + value.slice(1);
      return formated;
    },
    invertIMG:function(){
        if(this.isFront){
            this.currentImg=this.pokemon.back
            this.isFront=false

        }else{
            this.currentImg=this.pokemon.front
            this.isFront=true
        }
    }
  },
};
</script>

<style scoped>
    .poke{
        margin: 2% 0 0 0;
    }
</style>