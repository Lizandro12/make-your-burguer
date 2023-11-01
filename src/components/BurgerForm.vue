<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burger__form" @submit="createBurger">

                <div class="input__container">
                    <label for="name">Nome do cliente</label>
                    <input type="text" name="name" id="name" v-model="nome" placeholder="Digite o seu nome" class="input__name">
                </div>

                <div class="input__container">
                    <label for="pao">Escolha o Pão</label>
                    <select name="pao" id="pao" v-model="pao">
                    <option value="null">--Selecione o seu pão--</option>
                    <option :value="pao.tipo" v-for="pao in paes" :key="pao.id">{{pao.tipo}}</option>
                    </select>
                </div>

               
                <div class="input__container">
                    <label for="carne">Escolha a Carne</label>
                    <select name="carne" id="carne" v-model="carne">
                    <option value="null">--Selecione o tipo de carne--</option>
                    <option :value="carne.tipo" v-for="carne in carnes" :key="carne.id">{{carne.tipo}}</option>
                    </select>
                </div>

                <div class="input__container" id="opcionais__container">
                    <label for="opcionais" class="opcionais__title">Selecione os Opcionais</label>
                    <div class="check__box__container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" id="opcionais" :value="opcional.tipo" v-model="opcionais">
                        <span>{{opcional.tipo}}</span>
                    </div>
                </div>

                <div class="input__container">
                    <input type="submit" value="Criar meu Burger!" class="submit__btn">
                </div>

            </form>
        </div>
    </div>
</template>

<script>

import Message from './Message.vue';
export default {
    name: "BurgerForm",
    components:{
        Message
    },
    data (){
        return {
            paes:null,
            carnes:null,
            opcionaisdata: null,
            nome:null,
            pao:null,
            carne:null,
            opcionais:[],
            msg:null
        }
    },
    methods: {
        // Função que busca os ingredientes no backend 
        async getIngredients() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            
        //Insere os ingredientes nos inputs
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        //Cria os haburguers
        async createBurger(e){
            //Cancela o comportamento padrão do Formulario
            e.preventDefault();
            //Recebe os ingredientes selecionados para criar o hamburguer
            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }
            //Transforma eles em string para enviar ao backend
            const dataJson = JSON.stringify(data);

            //Envia o hamburguer formado para o backend
            const req = await fetch("http://localhost:3000/burgers" , {
                method:"POST",
                headers:{"Content-Type": "application/json"},
                body: dataJson
            });

            //Recebe a resposta da requisição
            const res = await req.json();
            console.log(res);

            this.msg = "Pedido realizado com sucesso"
            setTimeout(()=>{
                this.msg = "";
            },3000)

            this.resetVariables();

        },
        resetVariables(){

            this.pao = null;
            this.carne = null;
            this.nome = "";
            this.opcionais = []
        
        }
    },
    mounted(){
        this.getIngredients()
    }
}
</script>

<style scoped>

#burger__form{
    max-width: 300px;
    margin: 0 auto;

}

.input__container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label{
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input[type="text"],input[type="submit"], select {
    padding: 5px 10px;
    width: 300px;
}

.input__name{
    border:solid 1px silver;
    border-radius: 4px;
    transition: all .5s;
    outline: none;
    height: 45px;
}

.input__name:focus{
    border: solid 1px #fcba03;
}

.input__name::placeholder{
    font-size: 10pt;
    color: #8d8c8c;
}

#opcionais__container{
    flex-direction: row;
    flex-wrap: wrap;
}

.check__box__container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px ;
}

.check__box__container span, 
.check__box__container input{
    width: auto;
}

.check__box__container span{
    margin-left: 6px;
    font-weight: bold;
}

.opcionais__title{
    width: 100%;
}

.submit__btn{
    background-color: #222;
    color: #fbca03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
}

.submit__btn:hover{
    background-color: transparent;
    color: #222;
}


</style>