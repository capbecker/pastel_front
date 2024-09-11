<template>
  <Header></Header>
  <Form @handleFormSubmit="handleFormSubmit"></Form>
  <div class="divisoria" >Veja como será apresentado ao cliente</div>  
  <ListProdutos v-if="listProduto" :listProduto="listProduto"></ListProdutos>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import ListProdutos from './components/ListProdutos.vue'

export default {
  components: {Header,Form,ListProdutos},
  data() {
    return {
      listProduto:[]
    }
  }, 
  methods :{
    handleFormSubmit(produto) {   
      console.log(produto);   
      this.listProduto.push(produto);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;  
  background-image: url('./assets/images/pattern.png');
  background-repeat: repeat;
  z-index: -1;
  
}
.divisoria {
  color:rgb(160,52,0);
  font-size:22px;
  font-weight: bold; 
  font-style: italic;
}
</style>
