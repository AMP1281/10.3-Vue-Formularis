<template>

    <div>


        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>
                <input v-model="actualizar" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid': rojo }"/>
        </div>

            <small :class="{'text-secondary':obligGris, 'text-danger':obligVermell}">* Requerit. </small>
            <small :class="{'text-secondary':caracGris, 'text-danger':caracVermell}">5 dígits </small>
            <small :class="{'text-secondary':numGris, 'text-danger':numVermell}">Nomès números. </small>


        <!--<li v-for="(x, i) in lcodi" :key="i">  {{ x }} </li>-->
        

    </div>

</template>

<script>
export default {

    props: {

        codi: String,

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
            acodi:[],
            lcodi:[],

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
            this.lcodi=[];

            if(this.codi==""){
                this.lcodi.push("Aquest camp es obligatori");
                this.obligGris=false;
                this.obligVermell=true;
            }else{
                this.obligGris=true;
                this.obligVermell=false;
            }
            if(this.codi.length < 5 || this.codi.length > 5){ 
                this.lcodi.push("Aquest camp ha de contenir 5 caràcters");
                this.caracGris=false;
                this.caracVermell=true;
            }else{
                this.caracGris=true;
                this.caracVermell=false;
            }
            if(isNaN(this.codi)){
                this.lcodi.push("Aquest camp nomès pot contenir números.");
                this.numGris=false;
                this.numVermell=true;
            }else{
                this.numGris=true;
                this.numVermell=false;
            }
            if (!this.lcodi.length){
                this.isActive=false;
                this.verde=true;
                this.rojo=false;
            }
            if(this.lcodi.length > 0){
                this.isActive=false;
                this.verde=false;
                this.rojo=true;
            }
            //Envio errors del camp al pare per activar boto Enviar
            this.$emit('codiOk',this.lcodi);
        }
    },



    computed:{

        actualizar:{
            get(){
                return this.codi
            },  

            set(value){
                this.$emit('update:codi', value)
            }
        },
    },

}
</script>