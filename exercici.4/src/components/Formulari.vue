<template>

<div>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form class="w-75 bg-light border border-secondary p-5 rounded">

            <Test
             :nombre.sync="nombre" labelNom='Nom:'
             :mobil.sync="mobil" labelMobil='Mobil:'
             :codi.sync="codi" labelCodi='Codi Postal:'
             :mail.sync="mail" labelMail='E.mail:'
             :psw.sync="psw" labelPassword='Password:'
             :confirm.sync="confirm" labelConfirm='Confirmar Password:'
             @nombreOk="nOk=$event"
             @mobilOk="mOk=$event"
             @codiOk="cpOk=$event"
             @mailOk="eOk=$event"
             @pswOk="pOk=$event"
             @confirmOk="cOk=$event"
             />

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
            nombre:'',
            mobil:'',
            codi:'',
            mail:'',
            psw:'',
            confirm:'',

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
            if (this.nombre.length === 0 ||
                this.mobil.length === 0 ||
                this.codi.length === 0 ||
                this.mail.length === 0 ||
                this.psw.length === 0 ||
                this.confirm.length === 0){
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
