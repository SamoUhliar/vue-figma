<template>
    <div style="width:100%;height:100%">
        <input v-model="input">
        <button @click="evalx">eval</button>
        <div>{{output}}</div>
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
        (function () {
            console.log = function (message) {
                if (typeof message == 'object') {
                    this.output += (JSON && JSON.stringify ? JSON.stringify(message) : message) + '<br />';
                } else {
                    this.output += message + '<br />';
                }
            }
        })();
    },
    methods: {
        evalx(){ 
            try {
                console.oldLog = console.log;
                console.log = function(value)
                {
                    console.oldLog(value);
                    return value;
                };

                this.output = eval(this.input); 
                 console.warn(this.output)
            } catch (e) {    
                this.output = e.message;
            }
        }
    }

}
</script>
<style>

</style>
