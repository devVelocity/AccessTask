<template>
    <div class="errorBox fixed w-full duration-300 h-auto flex justify-center items-center pl-2 pr-2" :class="{errorActive : displayMessage != ''}">
        <div class="bg-red-800 pl-4 pr-4 pt-2 pb-2 rounded-md flex items-center justify-between w-auto h-auto">
            <h1 class="text-white"><span class="font-bold mr-2 inline-block">Error:</span>{{displayMessage}}</h1>
            <div @click="this.displayMessage = ''" class="ml-8 hover:cursor-pointer">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 stroke-white stroke-2" fill="none" viewBox="0 0 24 24" strokeWidth={2}>
                    <path strokeLinecap="round" strokeLinejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['errorMSG'],
    data(){
        return{
            displayMessage: this.errorMSG,
        }
    },
    mounted(){
        console.log(this.errorMSG)
    }
}
</script>

<style>
    .errorBox{
        bottom: -20%;
        pointer-events: none;
    }
    .errorActive{
        bottom: 3%;
        pointer-events: all;
    }
</style>