<template>
<div v-for="produto in listProduto" class="item" v-key="produto.titulo">
  <div class="container" >
    <div class="head">
        <!----><img :src="debugImageSrc(produto.arquivo)" alt="Imagem do Produto">

        <div class="titulo">"{{produto.titulo}}"</div>
        <div class="preco">{{formataPreco(produto.preco)}}</div>
    </div>
    <div class="body">
      <div class="sabor"><b>Sabor:</b> {{produto.sabor}}</div>
      <div class="descricao"><b>Descrição:</b> {{produto.descricao}}</div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['listProduto'],  
  data() {
    return {      
    }
  },
  methods :{
    debugImageSrc(arquivo) {
      if (arquivo && arquivo instanceof Blob) {
        return URL.createObjectURL(arquivo);
      }
      console.error('Erro: arquivo não é um Blob válido', arquivo);
      return '';
    },
    formataPreco(preco) {
      console.log(typeof preco);
      return `R$ ${parseFloat(preco).toFixed(2)}`;
    }
  } 
}

</script>

<style scoped>
.container {
  position: relative;
    width:800px;
    min-width: 800px;
    height: 150px;
    box-shadow: 0 0 50px rgba(0, 0, 0, 0.2);
    margin:10px;
    background:#fff;
    
    margin: auto;
    border-radius:40px;
    color:rgb(160,52,0);
    z-index: 1;
}
.head{
    background: rgb(228, 54, 54);
    border-radius:40px 40px 0 0;
    height: 80px;
    display: flex;
    color:rgb(255, 255, 255);
}

.titulo {
    display: inline;    
    margin-top: 0px;    
    margin-left: 50px;
    margin-right: auto;
    padding-top:20px;
    font-size:22px;
    font-weight: bold; 
    font-style: italic;
}
.preco{
    margin-left:auto;
    margin-top:15px;
    margin-right:50px;
    display: inline;
    text-align: right;
}

.body div{
   text-align: left;
   margin-left: 20px;
  
}
</style>

