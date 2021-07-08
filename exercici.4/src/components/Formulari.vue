<template>

<div>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form class="w-75 bg-light border border-secondary p-5 rounded">

            <Test :nombre.sync="nombrePadre" label='Nom:' @nombreOk="nOk=$event"/>
            
            <Test :mobil.sync="mobilPadre" label='Mobil:' @mobilOk="mOk=$event"/> 
            <Test :codi.sync="codiPadre" label='Codi Postal:' @codiOk="cpOk=$event"/>
            <Test :mail.sync="mailPadre" label='E.mail:' @maiOk="eOk=$event"/>
            <Test :psw.sync="pswPadre" label='Password:' @pswOk="pOk=$event"/>
            <Test :confirm.sync="confirmPadre" label='Confirmar Password:' @confirmOk="cOk=$event"/>

            <button type="submit" @click.prevent="openModal()" data-toggle="modal" data-target="#ModalBootstrap" class="btn btn-primary btn-block mt-5 rounded-pill" :class="{disabled: enableSubmitBtn}">Validar</button>

          </form>

        <ModalBootstrap v-if="showModal" @close="showModal=false"

            :nombre= 'nombre'
            :mobil= 'mobil'
            :codi= 'codi'
            :mail= 'mail'
            :psw= 'psw'
            :confirm= 'confirm'>

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
            nombrePadre:'',
            mobilPadre:'',
            codiPadre:'',
            mailPadre:'',
            pswPadre:'',
            confirmPadre:'',

            nOk:'',
            mOk:'',
            cpOk:'',
            eOk:'',
            pOk:'',
            cOk:'',

            disabled: true,

            showModal: false,
            }
    },

    //Desactivo botón hasta que todos los campos esten llenos y Ok(no hay errores en array)
    computed:{
        enableSubmitBtn() {
            if (this.nombrePadre.length === 0 ||
                this.mobilPadre.length === 0 ||
                this.codiPadre.length === 0 ||
                this.mailPadre.length === 0 ||
                this.pswPadre.length === 0 ||
                this.confirmPadre.length === 0){
                    return true;
                }

            if (this.nOk.length === 0 &&
                this.mOk.length === 0 &&
                this.cpOk.length === 0 &&
                this.eOk.length === 0 &&
                this.pOk.length === 0 &&
                this.cOk.length === 0)
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
