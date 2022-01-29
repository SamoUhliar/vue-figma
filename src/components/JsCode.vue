<template>
    <div style="width:100%;height:100%">
        <input v-model="input">
        <button @click="evalx">eval</button>
        <div id="error"></div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            selected:"",
            input:'',
            output:''
        }
    },
    mounted(){
        window.console.error = function(x){
            this.output=x
        }
    },
    methods: {
        evalx(){
            
            this.output=eval(this.input);

            
        }
    }

}
</script>
<style>

</style>
