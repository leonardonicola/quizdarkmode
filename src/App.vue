<template>
  <div ref="app" class="app">
    <label class="switch">
    <input type="checkbox" 
    v-model="toggle"/>
      <span class="slider round"></span>
    </label>  
    <Perguntas :toggle="toggle" :perguntas="perguntas"/>
  </div>
</template>

<script>
import Perguntas from './components/PerguntasVue.vue'
export default {
  components:{Perguntas},
  data(){
    return{
      toggle: false,
      perguntas:[
          {
              title:"O que é o Vue?",
              opcoes:[ 
              {opcao:"Lib"},
              {opcao: "Framework Front-End", correta:true},
              {opcao: "Plugin JS"},
              {opcao: "Preselector CSS"}
              ]
          },
          {
              title:"O que é HTML",
              opcoes:[
              {opcao: "Framework"},
              {opcao:"Linguagem de marcação", correta:true},
              {opcao: "Linguagem de programação"},
              {opcao: "Metodologia ágil"}
              ]
          },
          {
              title:"O que é JavaScript",
              opcoes:[
              {opcao: "Framework Back-End"},
              {opcao:"Preseletor CSS" },
              {opcao: "Linguagem de programação", correta:true},
              {opcao: "Biblioteca do Java"}
              ]
          }
          ]
    }
  },
  watch:{
    toggle(){
      if(this.toggle == true){
        this.$refs.app.style.backgroundColor = '#000'
      }else{
        this.$refs.app.style.backgroundColor = '#fff'
      }
    }
  }
}
</script>

<style>

#app, .app{
  height: 100vh;
}

.switch {
  position: absolute;
  right: 50px;
  top: 50px;
  display: inline-block;
  width: 60px;
  height: 34px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>