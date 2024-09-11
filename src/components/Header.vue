<template>     
     <div>
        <img class= "logo" :src="logo" alt="logo">
    </div>
</template>
<script>
export default {
    data() {
        return{
            logo: require('@/assets/images/Logo.svg')
        }
    }
}
</script>

<style scoped>
div{
    background-image: url('../assets/images/wave.svg');
    background-repeat: no-repeat;
    background-position: center 0%;      
    height:547px;   
    justify-content: center;
    align-items: center;    
    z-index: -1;
}
.logo {
    margin-top: 60px;
}

</style>