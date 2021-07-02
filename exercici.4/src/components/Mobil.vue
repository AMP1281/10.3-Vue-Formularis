<template>

    <div>

        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

        <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>

        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">10 dígits. </small>
            <small :class="{'text-secondary':numGris, 'text-danger':numVermell}">Nomès números. </small>

        <!--opció mostrar array-->
        <!--<li v-for="(x, i) in lmobil" :key="i">  {{ x }} </li>-->

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

        mobil: String,

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
            amobil:[],
            lmobil:[],

            isActive: true,
            verde: false,
            rojo: false,

            obligGris:true,
            obligVermell:false,

            caracGris:true,
            caracVermell:false,

            numGris:true,
            numVermell:false
        }
    },

    methods:{

        inline(){
            this.lmobil=[];

            if(this.mobil==""){
                this.lmobil.push("Aquest camp es obligatori");
                this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }
            if(this.mobil.length < 8 || this.mobil.length > 10){ 
                this.lmobil.push("Aquest camp ha de contenir 10 caràcters");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if(isNaN(this.mobil)){
                this.lmobil.push("Aquest camp nomès pot contenir números.");
                this.numGris=false;
                this.numVermell=true;
            }else{
                this.numGris=true;
                this.numVermell=false;
            }
            if (!this.lmobil.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lmobil.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('mobilOk',this.lmobil);
        }
    },

    computed:{

        actualizar:{
            get(){
                return this.mobil
            },  

            set(value){
                this.$emit('update:mobil', value)
            }
        },
    },

}
</script>