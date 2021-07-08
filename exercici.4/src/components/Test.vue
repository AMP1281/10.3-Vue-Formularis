<template>
<div>
    
        <!--Nom-->
        <div class="input-group">

            <span class="input-group-text font-weight-bold alert-primary">{{ labelNom }}</span>
             
            <input v-model="compNom" type="text" class= 'form-control' @blur="inlineN" :class="{ active: isActiveN, 'is-valid':verdeN , 'is-invalid':rojoN }"/>
        
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">

                        <small class="text-danger" v-for="(errorn, i) in lnom" :key="i"> {{ errorn }} </small>

                    </div>

                </div>

        </div>
        <!--End Nom-->

        <!--Telefon mòbil-->
        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ labelMobil }}</span>

            <input v-model="compMobil" type="text" class= 'form-control' @blur="inlineM" :class="{ active: isActiveM, 'is-valid':verdeM , 'is-invalid':rojoM }"/>

                <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">

                    <small class="text-danger" v-for="(errorm, i) in lmobil" :key="i"> {{ errorm }} </small>

                    </div>

                </div>

        </div>


        <!--End Telefon mòbil-->

        <!--Codi postal-->
        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ labelCodi}} </span>

            <input v-model="compCodi" type="text" class= 'form-control' @blur="inlineCP" :class="{ active: isActiveCP, 'is-valid':verdeCP , 'is-invalid': rojoCP }"/>
        
            <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">

                    <small class="text-danger" v-for="(errorcp, i) in lcodi" :key="i"> {{ errorcp }} </small>

                    </div>

                </div>

        </div>


        <!--End Codi postal-->

        <!--E.mail-->
        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ labelMail }}</span>

            <input v-model="compEmail" type="text" class= 'form-control' @blur="inlineE" :class="{ active: isActiveE, 'is-valid':verdeE , 'is-invalid': rojoE }"/>

                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">

            <small class="text-danger" v-for="(errore, i) in lmail" :key="i"> {{ errore }} </small>

                    </div>

                </div>

        </div>



        <!--End E.mail-->

        <!--Password-->
        <div class="input-group mt-4">

            <span class="input-group-text font-weight-bold alert-primary">{{ labelPassword }}</span>

        <input v-model="compPsw" type="text" class= 'form-control' @blur="inlineP" :class="{ active: isActiveP, 'is-valid':verdeP , 'is-invalid': rojoP }"/>
                    
                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">

            <small class="text-danger" v-for="(errorp, i) in lpsw" :key="i"> {{ errorp }} </small>

                                </div>

                </div>

        </div>
        <!--End Password-->

        <!--Confirmar Password-->
        <div class="input-group mt-4">

        <span class="input-group-text font-weight-bold alert-primary">{{ labelConfirm }}</span>

        <input v-model="compConf" type="text" class= 'form-control' @blur="inlineC" :class="{ active: isActiveC, 'is-valid':verdeC , 'is-invalid': rojoC }"/>
                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">

                    <div class="position-absolute">


            <small class="text-danger" v-for="(errorc, i) in lconfirm" :key="i"> {{ errorc }} </small>

                                            </div>

                </div>

        </div>
        <!--End Confirmar Password-->

</div>

</template>

<script>
export default {

    props: {
        nombre: {
            required: true,
            type: String,
            default:''
        },
        mobil: {
            required: true,
            default:0,
        },
        codi: {
            required: true,
            default:0,
        },
        mail: {
            required: true,
            default:'',
        },
        psw: {
            required: true,
            default:'',
        },
        confirm: {
            required: true,
            default:'',
        },
        labelNom:{
            type: String,
            required:true,
        },
        labelMobil:{
            type: String,
            required:true,
        },
        labelCodi:{
            type: String,
            required:true,
        },
        labelMail:{
            type: String,
            required:true,
        },
        labelPassword:{
            type: String,
            required:true,
        },
        labelConfirm:{
            type: String,
            required:true,
        },

    },

    data(){
        return{

            lnom:[],
            lmobil:[],
            lcodi:[],
            lmail:[],
            lpsw:[],
            lconfirm:[],

            active: true,
            verde: false,
            rojo: false,

            isActiveN: true,
            verdeN: false,
            rojoN: false,

            isActiveM: true,
            verdeM: false,
            rojoM: false,

            isActiveCP: true,
            verdeCP: false,
            rojoCP: false,

            isActiveE: true,
            verdeE: false,
            rojoE: false,

            isActiveP: true,
            verdeP: false,
            rojoP: false,

            isActiveC: true,
            verdeC: false,
            rojoC: false,

            obligGris:true,
            obligVermell:false,

            caracGris:true,
            caracVermell:false,

            numGris:true,
            numVermell:false,

            eobligatori:"* Requerit. ",
            enom:"Mínim 6 caràcters i màxim de 13",
            etelf:"Aquest camp ha de contenir 9 caràcters",
            ecodi:"Aquest camp ha de contenir 5 caràcters",
            enomnumeros:"El seu nom no pot contenir números.",
            enumeros:"No pot contenir lletres.",
            emajus:"Ha de contenir majúscules",
            eminus:"Ha de contenir minuscules",
            econfirm: "Ha de coincidir amb password. ",
            eEmail:"Ha de tenir format e.mail"

        }
    },

    methods:{

        //Nom
        inlineN(){

            this.lnom=[];
            
            this.obligatori(this.nombre,this.lnom);
            this.minMax(this.nombre,this.lnom);
            this.lletres(this.nombre,this.lnom);

            this.$emit('nombreOk',this.lnom);//Envio errors del camp al pare per activar boto Enviar

             if (!this.lnom.length){this.isActiveN=false;this.verdeN=true;this.rojoN=false;}
             if(this.lnom.length > 0){this.isActiveN=false;this.verdeN=false;this.rojoN=true;
            } 
        },

        //Telefon mòbil
        inlineM(){

            this.lmobil=[];

            this.obligatori(this.mobil,this.lmobil);
            this.minTel(this.mobil,this.lmobil);
            this.numeros(this.mobil,this.lmobil);

            this.$emit('mobilOk',this.lmobil);

            if (!this.lmobil.length){
                    this.isActiveM=false;
                    this.verdeM=true;
                    this.rojoM=false;
                }
            if(this.lmobil.length > 0){
                    this.isActiveM=false;
                    this.verdeM=false;
                    this.rojoM=true;
                }
        },

        //Codi postal
        inlineCP(){

            this.lcodi=[];

            this.obligatori(this.codi,this.lcodi);
            this.mincodi(this.codi, this.lcodi);
            this.numeros(this.codi,this.lcodi);

            this.$emit('codiOk',this.lcodi);

            if (!this.lcodi.length){
                    this.isActiveCP=false;
                    this.verdeCP=true;
                    this.rojoCP=false;
                }
                if(this.lcodi.length > 0){
                    this.isActiveCP=false;
                    this.verdeCP=false;
                    this.rojoCP=true;
                }
        },

        //E.mail
        inlineE(){

            this.lmail=[];

            this.obligatori(this.mail,this.lmail);
            this.email(this.mail,this.lmail);

            this.$emit('mailOk',this.lmail);

            if (!this.lmail.length){
                    this.isActiveE=false;
                    this.verdeE=true;
                    this.rojoE=false;
                }
                if(this.lmail.length > 0){
                    this.isActiveE=false;
                    this.verdeE=false;
                    this.rojoE=true;
                }
        },

        //Password
        inlineP(){

            this.lpsw=[];

            this.obligatori(this.psw,this.lpsw);
            this.minMax(this.psw,this.lpsw);
            this.may(this.psw,this.lpsw);
            this.min(this.psw,this.lpsw);

            this.$emit('pswOk',this.lpsw);

            //Envio campo password a Confirm para comparar
            //this.$root.$emit('iguales',this.psw);


            if (!this.lpsw.length){
                    this.isActiveP=false;
                    this.verdeP=true;
                    this.rojoP=false;
                }
                if(this.lpsw.length > 0){
                    this.isActiveP=false;
                    this.verdeP=false;
                    this.rojoP=true;
                }
        },

        //Confirmar Password
        inlineC(){

            this.lconfirm=[];

            this.obligatori(this.confirm,this.lconfirm);
            this.igual(this.confirm,this.lconfirm,this.psw);

            this.$emit('confirmOk',this.lconfirm);

            //Recibo campo password para poder comparar
            //mounted(){
            //  this.$root.$on('iguales',(message) => {
            //  this.campoPsw = message;
            //  });
            //},

            if (!this.lconfirm.length){
                    this.isActiveC=false;
                    this.verdeC=true;
                    this.rojoC=false;
                }

            if(this.lconfirm.length > 0){
                    this.isActiveC=false;
                    this.verdeC=false;
                    this.rojoC=true;
                }
        },

             //Validar camps obligatoris
            obligatori(campo,lista){
                if(!campo){
                    lista.push(this.eobligatori);
                } 
            },
            //Validar min max dígits 6-13
            minMax(campo,lista){ 
                if (campo.length < 6 || campo.length > 13){ 
                    lista.push(this.enom);
                }
            },
            //Validar min max dígits 9
            minTel(campo,lista){
                if(campo.length < 9 || campo.length > 9){ 
                    lista.push(this.etelf);
                }
            },
            //Validar min max dígits 5
            mincodi(campo,lista){
                if(campo.length < 5 || campo.length > 5){ 
                    lista.push(this.ecodi);
                }
            },
            //Validar mayuscules obligatories
            may(campo,lista){
                if (!/[A-Z]/.test(campo)){
                    lista.push(this.emajus);
                }
            },
            //Validar minuscules obligatories
            min(campo,lista){
                if (!/[a-z]/.test(campo)){
                    lista.push(this.eminus);
                }
            },
            //Validar que contingui lletres
            lletres(campo,lista){
                if(/[0-9]/.test(campo)){
                    lista.push(this.enomnumeros);
                }
            },
            //Validar que contingui números
            numeros(campo,lista){
                if(!/[0-9]/.test(campo)){
                    lista.push(this.enumeros);
                }
            },
            //Validar format e.mail
            email(campo,lista){
                if (!/[\w._-]+@[\wñ._-]+(?:\.[\w]+)+/.test(campo)) {
                    lista.push(this.eEmail);
                }
            },
            //Validar que dos inputs siguin identics
            igual(campo,lista,c){
                if(c != campo){
                    lista.push(this.econfirm);
                }
            },

            //Class Bootstrap (gris,vermell,verd)
/*             ValidacionVerde(campo, active, verde, rojo){
                if (!campo.length){
                    active=false,
                    verde=true,
                    rojo=false;
                }
            },

            ValidacionRojo(campo, active, verde, rojo){
                if(campo.length > 0){
                    active=false,
                    verde=false,
                    rojo=true;
                }
            }, */
    },


     computed:{

        compNom:{
            get(){
                return this.nombre;
            },  

            set(value){
                this.$emit('update:nombre', value)
            }
        },
        compMobil:{
            get(){
                return this.mobil
            },  

            set(value){
                this.$emit('update:mobil', value)
            }
        },
        compCodi:{
            get(){
                return this.codi
            },  

            set(value){
                this.$emit('update:codi', value)
            }
        },
        compEmail:{
            get(){
                return this.mail
            },  

            set(value){
                this.$emit('update:mail', value)
            }
        },
        compPsw:{
            get(){
                return this.psw
            },  

            set(value){
                this.$emit('update:psw', value)
            }
        },
        compConf:{
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

<style>

.input-group-text {
    min-width:25% !important;
}

</style>