<template>

<div>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form class="w-75 bg-light border border-secondary p-5 rounded">

            <Test label='Nom:' @nombreOk="nOk=$event"/>
            <Test label='Mobil:' @mobilOk="mOk=$event"/> 
            <Test label='Codi Postal:' @codiOk="cpOk=$event"/>
            <Test label='E.mail:' @mailOk="eOk=$event"/>
            <Test label='Password:' @pswOk="pOk=$event"/>
            <Test label='Confirmar Password:' @confirmOk="cOk=$event" :confPadrepsw="pOk.valorPsw"/><!--Envio psw en :confPadrepsw-->

            <button type="submit" @click.prevent="openModal()" data-toggle="modal" data-target="#ModalBootstrap" class="btn btn-primary btn-block mt-5 rounded-pill" :class="{disabled: enableSubmitBtn}">Validar</button>

          </form>

        <ModalBootstrap v-if="showModal" @close="showModal=false"

            :nombre= 'nOk.valorNombre'
            :mobil= 'mOk.valorMobil'
            :codi= 'cpOk.valorCodi'
            :mail= 'eOk.valorMail'
            :psw= 'pOk.valorPsw'
            :confirm= 'cOk.valorConf'>

        </ModalBootstrap>

    </div>

</div>

</template>

<script>

import Test from './Test.vue'
import ModalBootstrap from './ModalBootstrap.vue'

export default {
    name: 'Formulari',

    components:{
        ModalBootstrap,
        Test
    },

    data(){
        return{
            pswPadreConf:'',

            value:'',

            nOk:{
                arrayNombre:'',
                valorNombre:''
            },
            mOk:{
                arrayMobil:'',
                valorMobil:''
            },
            cpOk:{
                arrayCodi:'',
                valorCodi:''
            },
            eOk:{
                arrayMail:'',
                valorMail:''
            },
            pOk:{
                arrayPsw:'',
                valorPsw:''
            },
            cOk:{
                arrayConf:'',
                valorConf:''
            },

            disabled: true,

            showModal: false,
            }
    },

    //Desactivo botón hasta que todos los campos esten llenos y Ok(no hay errores en array)
    computed:{
        enableSubmitBtn() {
            if (this.nOk.valorNombre.length === 0 ||
                this.mOk.valorMobil.length === 0 ||
                this.cpOk.valorCodi.length === 0 ||
                this.eOk.valorMail.length === 0 ||
                this.pOk.valorPsw.length === 0 ||
                this.cOk.valorConf.length === 0){
                    return true;
                }

            if (this.nOk.arrayNombre.length === 0 &&
                this.mOk.arrayMobil.length === 0 &&
                this.cpOk.arrayCodi.length === 0 &&
                this.eOk.arrayMail.length === 0 &&
                this.pOk.arrayPsw.length === 0 &&
                this.cOk.arrayConf.length === 0)
                {
                return false;
            }else{
                return true;
            }
        },

    },

    //Si el botón no esta ok(todas validaciones ok) no se abre modal
    methods:{
        openModal(){
            if (!this.enableSubmitBtn){
                this.showModal = true;
                }
            else{
                this.showmodal= false;
            }
        },

     },
}

</script>

<style>


</style>
