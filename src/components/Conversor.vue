<template>
    <div class="conversor">
        <h2>{{moedaA}} Para {{moedaB}}</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA"> 
        <input type="button" value="Converter" v-on:click="converter">
        <h2>{{ moedaB_value }}</h2>
    </div>
</template>

<script>
export default {
    name: "conversor",
    props: ["moedaA","moedaB"],
    data() {
        return{
            moedaA_value : "",
            moedaB_value : 0
        };
    },
    methods: {
        //Converte o valor das moedas
        converter(){
            //Api de Conversao
            let de_para = this.moedaA + "-" + this.moedaB; 
            console.log(de_para);
            let url ="https://economia.awesomeapi.com.br/last/"+de_para;

        fetch(url).then(res => { return res.json();})
                  .then(json => {
                      let cotacao = json[de_para].ask;
                      this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);  
                  })

        }
    },
};
</script>

<style scoped>

</style>