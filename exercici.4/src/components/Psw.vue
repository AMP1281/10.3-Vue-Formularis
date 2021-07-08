<template>

    <div>


        <div class="input-group">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

        <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>

        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">Mínim de 6 i màxim de 13 dígits. </small>
            <small :class="{'text-secondary':numGris, 'text-danger':numVermell}">Ha de contenir minúscules. </small>
            <small :class="{'text-secondary':mayGris, 'text-danger':mayVermell}">Ha de contenir majúscules. </small>

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

            mayGris:true,
            mayVermell:false,
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
            if(this.psw.length < 6 || this.psw.length > 13){ 
                this.lpsw.push("Aquest camp ha de contenir entre 6 i 13 caràcters.");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if(!/[a-z]/.test(this.psw)){
                this.lpsw.push("Aquest camp Ha de contenir minúscules.");
                this.numGris=false;
                this.numVermell=true;
            }else{
                this.numGris=true;
                this.numVermell=false;
            }
            if(!/[A-Z]/.test(this.psw)){
                this.lpsw.push("Aquest camp Ha de contenir majúscules.");
                this.mayGris=false;
                this.mayVermell=true;
            }else{
                this.mayGris=true;
                this.mayVermell=false;
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