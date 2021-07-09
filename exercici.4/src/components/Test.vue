<template>
<div>
    
    <div class="input-group mt-4">

        <span class="input-group-text font-weight-bold alert-primary">{{ label }}</span>
            
        <input v-model="value" type="text" class= 'form-control' @blur="inline" :class="{ active: isActive, 'is-valid':verde , 'is-invalid':rojo}"/>
        
        <div class="container position-relative col-md-12" style="height: 0.9em !important;">

            <div class="position-absolute">

                    <li class="text-danger list-inline-item" v-for="(errorn, i) in lerrores" :key="i"><small> {{ errorn }} </small></li>

            </div>

        </div>

    </div>

</div>

</template>

<script>
export default {

    props:  ['label','confPadrepsw'],

    data(){
        return{

            value:'',

            lerrores:[],

            lnom:[],
            lmobil:[],
            lcodi:[],
            lmail:[],
            lpsw:[],
            lconfirm:[],

            isActive: true,
            verde: false,
            rojo: false,

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

        inline(){

            this.lnom=[];
            this.lmobil=[];
            this.lcodi=[];
            this.lmail=[];
            this.lpsw=[];
            this.lconfirm=[];

            //Nom
            if(this.label == 'Nom:'){

                //Validacio
                this.obligatori(this.value,this.lnom);
                this.minMax(this.value,this.lnom);
                this.lletres(this.value,this.lnom);

                this.$emit('nombreOk',{arrayNombre:this.lnom, valorNombre:this.value});//Envio errors i valor del camp al pare per activar boto Enviar

                !this.lnom.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));//Activo class de Bootstrap invalid o valid depenent si hi han errors en el array

                this.lerrores=this.lnom//Igualo lerrores a lnom pq en cada input mostri els errors corresponents.
            }

            //Mobil
            if(this.label == 'Mobil:'){

                this.obligatori(this.value,this.lmobil);
                this.minTel(this.value,this.lmobil);
                this.numeros(this.value,this.lmobil);

                this.$emit('mobilOk',{arrayMobil:this.lmobil, valorMobil:this.value});

                !this.lmobil.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));
                
                this.lerrores=this.lmobil
            }
            //Codi postal
            if(this.label == 'Codi Postal:'){

                this.obligatori(this.value,this.lcodi);
                this.mincodi(this.value, this.lcodi);
                this.numeros(this.value,this.lcodi);

                this.$emit('codiOk',{arrayCodi:this.lcodi,valorCodi:this.value});

                !this.lcodi.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));

                this.lerrores=this.lcodi
            }
            //E.mail
                if(this.label == 'E.mail:'){

                this.obligatori(this.value,this.lmail);
                this.email(this.value,this.lmail);

                this.$emit('mailOk',{arrayMail:this.lmail, valorMail:this.value});

                !this.lmail.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));

                this.lerrores=this.lmail
            }
            //Password
            if(this.label == 'Password:'){

                this.obligatori(this.value,this.lpsw);
                this.minMax(this.value,this.lpsw);
                this.may(this.value,this.lpsw);
                this.min(this.value,this.lpsw);

                this.$emit('pswOk',{arrayPsw:this.lpsw, valorPsw:this.value});

                !this.lpsw.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));

                this.lerrores=this.lpsw
            }
            //Confirmar Password
            if(this.label == 'Confirmar Password:'){

                this.obligatori(this.value,this.lconfirm);
                this.igual(this.value,this.lconfirm,this.confPadrepsw);//Utilizo el prop recibido del padre confPadrepsw para comparar

                this.$emit('confirmOk',{arrayConf:this.lconfirm, valorConf:this.value});

                !this.lconfirm.length? ((this.isActive=false), (this.verde=true), (this.rojo=false)) : ((this.isActive=false),(this.verde=false),(this.rojo=true));

                this.lerrores=this.lconfirm;
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
    },

}

</script>

<style>

.input-group-text {
    min-width:25% !important;
}

</style>