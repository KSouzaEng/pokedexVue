<template>
    <div id="pokemon">
    <div class="card">
  <div class="card-image">
    <figure >
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
      </div>
      <div class="media-content">
        <p class="title is-4">{{num}}-{{name | upper}}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
        <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
    </div>
  </div>
</div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    
    props:{
        name:String,
        url:String,
        num: Number
    },
    filters:{
        upper(value){
            var newName = value[0].toUpperCase()+ value.slice(1)
            return newName
        }
    },
    data(){
        return{
            isFront: true,
            currentImg:'',
            pokemon:{
                type:'',
                front:'',
                back:''
            }
        }
    },
    created(){
        axios.get(this.url).then(res =>{
            console.log(res)
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            console.log(this.pokemon.front)
            this.currentImg = this.pokemon.front
        })
    },
    methods:{
        mudarSprite(){
            if(this.isFront){
                this.isFront = false
                this.currentImg = this.pokemon.back
            }else{
                this.isFront = true
                this.currentImg = this.pokemon.front

            }
        }
    }
}
</script>
<style>
#pokemon{margin-top:2%}
</style>