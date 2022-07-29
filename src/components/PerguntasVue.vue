<template>
    <div class="main">
        <div v-for="pergunta in perguntas.slice(n, n+1)" :key="pergunta" 
        class="main__quiz" :class="toggle ? 'dark':''" >

            <div  class="main__container-header" :class="toggle ? 'darkHeader' : ''">
                <h1 id="title">{{pergunta.title}}</h1>
            </div>

            <h1>Questão: {{n}}/{{perguntas.length}}</h1>

            <ul class="main__opcoes">
                <li v-for="(opc,index) in pergunta.opcoes" :key="index" 
                @click="selecionarOpcao(opc)"
                :class="respondida ? check(opc) : ''"
                >{{opc.opcao}}</li>
            </ul>
            
        </div>

        <button v-if="n < perguntas.length-1" @click="next" 
        :disabled="!respondida" class="main__btn" :class="toggle ? 'dark':''">PRÓXIMA</button>

        <button v-if="n == perguntas.length-1" @click="finalizar" 
        :disabled="!respondida" class="main__btn" :class="toggle ? 'dark':''">FINALIZAR</button>
        
        <div v-if="scoreshow" class="resultado">
            <h1 :class="toggle ? 'darkTitle':''">SEU SCORE: {{score}}/{{perguntas.length}}</h1>
            <button @click="restart" class="main__btn" :class="toggle ? 'dark':''">REINICIAR</button>
        </div>
    </div>
</template>

<script>
export default {
    props:{toggle: Boolean},
    data(){
        return{
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
            ],
            n:0,
            score:0,
            respondida: false,
            scoreshow: false
        }
    },
    methods:{
        
        selecionarOpcao(opc){
            switch(this.respondida){
                case false:
                    if(opc.correta){
                        this.score++
                        this.respondida = true
                    }else{
                        this.respondida = true
                    }
                    break;
                case true:
                    break;
            }
        },
        check(opc){
            if(opc.correta){
                return 'correta'
            }else{
                return 'incorreta'
            }
        },
        next(){
            this.n++
            this.respondida = false;
        },
        finalizar(){
            this.n++
            this.scoreshow = true
        },
        restart(){
            Object.assign(this.$data, this.$options.data())
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
    margin: 0;
    letter-spacing: 2px;
    transition: all .5s ease-out;
}

.dark,
.darkHeader{
    color: #000 !important;
}

.darkTitle{
    color: #fff;
}

.dark{
    background-color: #fff !important;
}

.darkHeader{
    background-color: rgb(180, 180, 180) !important;
}

.main{
    display: grid;
    justify-items: center;
    grid-template-columns: 1fr;
}

.main__container-header{
    display: flex;
    width: 100%;
    height: 20%;
    margin-bottom: 15px;
    border-bottom: 1px solid #e7eae0;
    justify-content: center;
    align-items: center;
    color: #fff;
    background-color: #000000;
    border-radius: 10px 10px 0px 0px;
}

.main__quiz{
    display:flex;
    width: 40%;
    height: 85%;
    background-color: rgb(43, 43, 43);
    color: #fff;
    flex-direction: column;
    align-items: center;
    border: 1px solid #e7eae0;
    border-radius: 10px;
    margin-top: 70px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
}

#title{
    margin: 50px auto;
}

ul {
    display: flex;
    flex-direction: column;
    width: 80%;
    margin-top: 20px;
    padding: 0;
}

li {
    list-style: none;
    line-height: 2;
    border: 1px solid #cdd2d2;
    margin-bottom: 20px;
    border-radius: 15px;
    cursor: pointer;
    padding: 10px;
}

li:hover {
    /*transform: scale(1.1);*/
    background-color: #e7eae0;
}

li.correta,
li.incorreta{
    color: white;
    font-weight: 600;
}

li.correta {
    border: 1px solid rgb(74, 219, 74);
    background-color: rgb(74, 219, 74);
    
}

li.incorreta {
    border: 1px solid rgb(240, 117, 100);
    background-color: rgb(240, 117, 100);
}

.main__btn{
    width: fit-content;
    height: 35px;
    margin-bottom: 10px;
    padding: 10px;
    border: 0;
    color: #fff;
    font-size: 1.2em;
    border-radius: 15px;
    align-items: center;
    cursor: pointer;
    background-color: #535353f5;
}

.main__btn:hover{
    background-color: rgb(46, 46, 46);
    transform: scale(1.05);
}

.check {
    color: rgb(74, 219, 74);
}

.resultado{
    display: flex;
    flex-direction: column;
    justify-items: center;
    align-items: center;
    margin: 200px;
}

</style>