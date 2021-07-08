<template>

    <div>


        <div class="input-group">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

        <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>

        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">Introdueix una direcció de correu electrónic vàlida. </small>

    </div>

</template>

<script>

export default {

    props: {

        mail: String,

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
            amail:[],
            lmail:[],

            isActive: true,
            verde: false,
            rojo: false,

            obligGris:true,
            obligVermell:false,

            caracGris:true,
            caracVermell:false,
        }
    },

    methods:{

        inline(){

            this.lmail=[];

            if(this.mail==""){
                this.lmail.push("Aquest camp es obligatori");
                 this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }

            if (!/[\w._-]+@[\wñ._-]+(?:\.[\w]+)+/.test(this.mail)){
                this.lmail.push("Introdueix una direcció de correu electrónic vàlida.");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if (!this.lmail.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lmail.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('mailOk',this.lmail);
        }
    },

    computed:{

        actualizar:{
            get(){
                return this.mail
            },  

            set(value){
                this.$emit('update:mail', value)
            }
        },
    },

}
</script>