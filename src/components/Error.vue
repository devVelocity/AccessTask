<template>
    <div class="bg-black z-20 bg-opacity-50 fixed w-full h-full duration-200 background" :class="{bgActive : errorMSG != ''}" @click="$emit('clearError')"></div>
    <div class="errorBox fixed w-full duration-300 h-auto flex justify-center items-center pl-2 pr-2 z-30" :class="{errorActive : errorMSG != ''}">
        <div class="bg-red-800 pl-4 pr-4 pt-2 pb-2 rounded-md flex items-center justify-between w-auto h-auto flex-col">
            <h1 class="text-white"><span class="font-bold mr-2 inline-block">Error:</span>{{errorMSG}}</h1>
            <br>
            <h2 class="text-white mt-4">Click outside of this box to close.</h2>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        errorMSG: String,
    },
    data(){
        return{
            displayMessage: this.errorMSG,
        }
    },
    mounted(){
        console.log(this.errorMSG)
    },
    // watch: { 
    //   	errorMSG: function(newVal, oldVal) { // watch it
    //       console.log('Prop changed: ', newVal, ' | was: ', oldVal)
    //     }
    // }
}
</script>

<style>
    .errorBox{
        top: -20%;
        pointer-events: none;
    }
    .errorActive{
        top: 30%;
        pointer-events: all;
    }
    .background{
        opacity: 0%;  
        pointer-events: none;
    }
    .bgActive{
        opacity: 100%;
        pointer-events: all;
    }
</style>