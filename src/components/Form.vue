<template>
<div class="container" >
    <img class= "pastel-paralax" :src="srcPasteis[1]" alt="pastel-paralax">    
    <img class= "pasteis" :src="srcPasteis[0]" alt="pasteis">    
    <form  @submit.prevent="handleFormSubmit" class="form">
        <div class="head">
            <div class="headTitle">Monte aqui o seu cadápio. O que está esperando?</div>
            <div class="categoria">
                Comida
                <input type="range" min="0" max="1" class="slider"> 
                Bebida
            </div>
        </div>
        <div class="body">
            <input type="text" class="titulo" v-model="formulario.titulo" required placeholder="Título do pedido">
            <input type="text" class="sabor" v-model="formulario.sabor" required placeholder="Sabor">
            <input type="text" class="preco" v-model="formulario.preco" required placeholder="R$" pattern="[0-9]+([.][0-9]{0,2})?">
            <textarea rows= 2 class="descricao" v-model="formulario.descricao" placeholder="Descrição"></textarea>
            <input type="file" class="arquivo" ref="fileInput" @change="handleImageChange" required accept=".png, .jpg, .jpeg"
                placeholder="Jogue aqui o arquivo de imagem do seu pastel ou clique para localizar a pasta">
        </div>
        <br><a href="#" class="limpar" @click.prevent="limpar">Limpar</a> <button type="submit" class="cadastrar">Cadastrar</button>
    </form>    
</div>    
</template>

<script>
export default {
    data() {
        return{
            formulario: {
                tipo:'',
                titulo:'',
                sabor:'',
                preco:'',
                descricao:'',
                arquivo: null
            },
            img:'',
            srcPasteis:[
                require('@/assets/images/pasteis-img.png'),
                require('@/assets/images/pastel-paralax.png')
            ]    
        }        
    }, 
    methods :{
        handleImageChange(event) {
            const file = event.target.files[0];
            const formatosPermitidos = ["image/png", "image/jpeg", "image/jpg"];
            const tipoDoArquivo = file.type;
            if (formatosPermitidos.includes(tipoDoArquivo.toLowerCase())) {
                this.formulario.arquivo = file;
            } else {
                const inputFile = this.$refs.fileInput;
                if (inputFile) {
                    inputFile.value = '';
                }
            }
        },
        limpar() {
            this.formulario.tipo = '';
            this.formulario.titulo = '';
            this.formulario.sabor = '';
            this.formulario.preco = '';
            this.formulario.descricao = '';
            this.formulario.arquivo = null;

            const inputFile = this.$refs.fileInput;
            if (inputFile) {
                inputFile.value = '';
            }
        },
        handleFormSubmit() {                
            var formTemp = {
                "tipo" : this.formulario.tipo,
                "titulo" : this.formulario.titulo,
                "sabor" : this.formulario.sabor,
                "preco" : this.formulario.preco,
                "descricao" : this.formulario.descricao,
                "arquivo": this.formulario.arquivo
            };
            this.limpar();
            this.$emit('handleFormSubmit',formTemp);
        }
    }
}
</script>

<style scoped>
.container  {
    /*display: flex;
    justify-content: center;
    align-items: center;  */
    position:relative;
    top:-500px; 
    z-index: 1;    
}
.pastel-paralax {
    position:relative;
    top:-100px;
    left:-350px;
    z-index: 2; 
    user-select: none;
    pointer-events: none;    
}
.pasteis{
    position:relative;
    top:-130px;
    left:185px;
    z-index: 0;
    
}
.form{
    position: relative;
    width:1100px;
    min-width: 1100px;
    height: 420px;
    box-shadow: 0 0 50px rgba(0, 0, 0, 0.2);
    background:#fff;
    
    margin: -305px auto;
    border-radius:40px;
    color:rgb(160,52,0);
    z-index: 1;
}


.head{
    /*margin: -205px;*/
    background: rgb(255, 202, 0);
    border-radius:40px 40px 0 0;
    height: 80px;
    display: flex;
}
.headTitle {
    display: inline;    
    margin-top: 0px;    
    margin-left: 50px;
    margin-right: auto;
    padding-top:20px;
    font-size:22px;
    font-weight: bold; 
    font-style: italic;
    /*height: 50px;
    text-decoration: bold;*/
}
.categoria{
    margin-left:auto;
    margin-top:15px;
    margin-right:50px;
    display: inline;
    text-align: right;
}
.slider {
    width: 30px;  

}

/* se eu tiver tempo mexo nisso*/
.slider::-webkit-slider-thumb {  
  /*-webkit-appearance: none;
  appearance: none;
  width: 20px; 
  height: 20px; 
  background:  rgb(228, 54, 54);
  cursor: pointer;
  border-radius: 50%; */
}
.body{
    padding: 0% 2% 2%;
    display: flex;
    flex-wrap: wrap;
    margin-top: -20px;    
}
.body input,textarea{
  margin-right: 1%;
  color:rgb(240,142,142);
  border: 2px solid rgb(240,142,142);
  border-radius: 13px;
  text-decoration: none;
  font-size: 15px;
  padding:11px 20px 8px ;
  margin-bottom: 2%;
  
}
.body input::placeholder{
    color:rgb(160,52,0); 
}

.titulo {    
    width: 32%;
}
.sabor {
    width: 35%;
}
.preco {
    width: 15%;
}
.descricao {    
    width: 92%;
    height: 80px;
    vertical-align: top;
    resize: none;

}

.arquivo[type="file"] {
}

a, .cadastrar{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 15px 60px;    
    background: #aaa;
    border-radius: 50px;
    font-size: 20px;
    letter-spacing: 1px;
    font-weight: bold;
    text-decoration: none;
    
}
.limpar{
    background: rgb(228, 54, 54);
    color:rgb(255, 255, 255);
}
.cadastrar{
    border: none;
    background: rgb(255, 202, 0);
    color:rgb(160,52,0);
}


</style>
