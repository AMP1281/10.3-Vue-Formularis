<template>

    <div>


        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>

        <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>

        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">Ha de coincidir amb password. </small>


    </div>

</template>

<script>
export default {

    props: {

        confirm: String,

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
            
            aconfirm:[],
            lconfirm:[],

            campoPsw: '',

            isActive: true,
            verde: false,
            rojo: false,

            obligGris:true,
            obligVermell:false,

            caracGris:true,
            caracVermell:false,

        }
    },

    //Recibo campo password para poder comparar
    mounted(){
        this.$root.$on('iguales',(message) => {
            this.campoPsw = message;
        });
    },

    methods:{

        inline(){
            this.lconfirm=[];


            if(this.confirm==""){
                this.lconfirm.push("Aquest camp es obligatori");
                this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }

            if(this.confirm != this.campoPsw){
                this.lconfirm.push("Ha de coincidir amb password.");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }

            if (!this.lconfirm.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lconfirm.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('confirmOk',this.lconfirm);
        }
    },

    computed:{

        actualizar:{
            get(){
                return this.confirm
            },  

            set(value){
                this.$emit('update:confirm', value)
            }
        },
    },

}
</script>