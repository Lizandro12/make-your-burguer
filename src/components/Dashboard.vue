<template>
    <div class="burger__table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div class="burger__table__header">
                <div class="order__id">Numero</div>
                <div class="">Cliente:</div>
                <div class="">Pão:</div>
                <div class="">Carne:</div>
                <div class="">Opcionais:</div>
                <div class="">Ações:</div>
            </div>
            <div class="burger__table__rows">
                <div class="burger__table__row" v-for="burger in burgers" :key="burger.id">
                    <div class="order__number">{{ burger.id }}</div>
                    <div class="">{{burger.nome}}</div>
                    <div class="">{{burger.pao}}</div>
                    <div class="">{{burger.carne}}</div>
                    <div class="">
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
                        </ul>
                    </div>
                    <div class="order__number">
                        <select name="status" class="status" @change="update($event, burger.id)">
                            <option value="">--Status--</option>
                            <option :value="statu.tipo" v-for="statu in status" :key="statu.id" :selected="burger.status == statu.tipo">{{ statu.tipo }}</option>
                        </select>
                        <button class="delete__pedido" @click="deletar(burger.id)">Cancelar</button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>


<script>
import Message from './Message.vue';

export default {
    name: "Dashboard",
    components: {
        Message,
    },
    data (){
        return {
            burgers:null,
            burgerId:null,
            status:[],
            msg:null
        }
    },
    //Busca os dados do backend para que seja imprimido na tela
    methods: {
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();

            this.burgers = data;

            this.getStatus();

            
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();

            this.status = data
        },
        async deletar(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();
            
            //Mensagem de confirmação de remoção do pedido
            this.msg = "Pedido removido com sucesso"
            setTimeout(()=>{
                this.msg = "";
            },3000)

            this.getPedidos();
        },
        async update(event, id){
            const option = event.target.value;

            const dataJson = JSON.stringify({
                status: option
            });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method:"PATCH",
                headers:{"Content-Type": "application/json"},
                body:dataJson
            });

            const res = await req.json();

            this.msg = `O pedido nº ${res.id} foi atualizado para ${res.status}`
            setTimeout(()=>{
                this.msg = "";
            },3000)
        }
    },
    mounted() {
        this.getPedidos()
    }
}


</script>


<style scoped>

.burger__table{
    max-width: 1300px;
    margin: 0 auto;
}

.burger__table__header,
.burger__table__rows,
.burger__table__row{
    display: flex;
    flex-wrap: wrap;
}

.burger__table__header{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

.burger__table__header div,
.burger__table__row div{
    width: 16%;
    text-align: center;

}

.burger__table__row{
    width: 100%;
    height: 150px;
    padding: 12px;
    border-bottom: solid 1px #ccc;
    display: flex;
    align-content: center;
}


select {
    padding:6px ;
    margin-right: 8px;
    border-radius: 4px;
}

.delete__pedido{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 6px;
    font-size: 13px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
    border-radius: 4px;
}

.delete__pedido:hover{
    color: #222;
    background-color: transparent;
}

li{
    list-style: none;
}

</style>