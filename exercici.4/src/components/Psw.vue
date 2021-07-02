<template>

    <div>


        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

        <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>

        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">Mínim de 6 i màxim de 13 dígits. </small>
            <small :class="{'text-secondary':numGris, 'text-danger':numVermell}">Ha de contenir majúscules i minúsvules. </small>
        
        
        <!--<li v-for="(x, i) in lpsw" :key="i">  {{ x }} </li>-->

        <!--
        <p v-if="!nombre">Aquest camp es obligatori</p>
        <p v-if="nombre.length < 6 || nombre.length > 13">Aquest camp ha de contenir entre 6 i 13 caràcters.</p>
        <p v-if="/[0-9]/.test(nombre)">El seu nom no pot contenir números.</p> 
        -->

    </div>

</template>

<script>
export default {

    props: {

        psw: String,

        id:{
            type: String,
            required: true,
        },

        label:{
            type: String,
            required:true,
        },
        type:{
            type:String,
            required:true,
        },
    },

    data(){
        return{
            apsw:[],
            lpsw:[],

            isActive: true,
            verde: false,
            rojo: false,

            obligGris:true,
            obligVermell:false,

            caracGris:true,
            caracVermell:false,

            numGris:true,
            numVermell:false,
        }
    },

    methods:{

        inline(){

            this.lpsw=[];

            if(this.psw==""){
                this.lpsw.push("Aquest camp es obligatori");
                this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }
            if(this.psw.length < 5 || this.psw.length > 14){ 
                this.lpsw.push("Aquest camp ha de contenir entre 6 i 13 caràcters.");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if(!/[A-z]/.test(this.psw)){
                this.lpsw.push("Aquest camp Ha de contenir majúscules i minúsvules.");
                this.numGris=false;
                this.numVermell=true;
            }else{
                this.numGris=true;
                this.numVermell=false;
            }
            //Envio campo password a Confirm para comparar
            this.$root.$emit('iguales',this.psw);

            if (!this.lpsw.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lpsw.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('pswOk',this.lpsw);
        }
    },

    computed:{

        actualizar:{
            get(){
                return this.psw
            },  

            set(value){
                this.$emit('update:psw', value)
            }
        },
    },

}
</script>