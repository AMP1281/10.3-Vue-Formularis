<template>

    <div>

        <div class="input-group">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

            <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid':rojo }"/>
        
        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">Mínim de 6 i màxim de 13 dígits. </small>
            <small :class="{'text-secondary':numGris, 'text-danger':numVermell}">Nomès text </small>
        
        <!--opció mostrar array-->
        <!--<li v-for="(x, i) in lnom" :key="i">  {{ x }} </li>-->

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

        nombre: String,

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
            anom:[],
            lnom:[],

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

            this.lnom=[];

            if(this.nombre==""){
                this.lnom.push("Aquest camp es obligatori");
                this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }
            if(this.nombre.length < 6 || this.nombre.length > 13){ 
                this.lnom.push("Aquest camp ha de contenir entre 6 i 13 caràct");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if(/[0-9]/.test(this.nombre)){ 
                this.lnom.push("El seu nom no pot contenir números.");
                this.numGris=false;
                this.numVermell=true;
            }else{
                this.numGris=true;
                this.numVermell=false;
            }
            if (!this.lnom.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lnom.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('nombreOk',this.lnom);
        }
    },

    computed:{

        actualizar:{
            get(){
                return this.nombre
            },  

            set(value){
                this.$emit('update:nombre', value)
            }
        },
    },


}
</script>

<style>

.input-group-text {
    min-width:25% !important;
}

</style>