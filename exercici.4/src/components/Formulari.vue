<template>

<div>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form class="w-75 bg-light border border-secondary p-5 rounded">
            
            <Nom :nombre.sync="nombre" label='Nom:' type='text' id='fname' @nombreOk="nOk=$event"/>

            <Mobil :mobil.sync="mobil" label='Telèfon mòbil:' type='text' id='lmobil' @mobilOk="mOk=$event"/>

            <Codi :codi.sync="codi" label='Codi Postal:' type='text' id='lcodiPostal' @codiOk="cpOk=$event"/>

            <Mail :mail.sync="mail" label='E.mail:' type='text' id='lemail' @mailOk="eOk=$event"/>

            <Psw :psw.sync="psw" label='Password:' type='password' id='lpasw' @pswOk="pOk=$event"/>

            <Confirm :confirm.sync="confirm" label='Confirmar Password:' type='password' id='lconfirm' @confirmOk="cOk=$event"/>
        

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

import Nom from './Nom.vue'
import Mobil from './Mobil.vue'
import Codi from './Codi.vue'
import Mail from './Mail.vue'
import Psw from './Psw.vue'
import Confirm from './Confirm.vue'
import ModalBootstrap from './ModalBootstrap.vue'


export default {
    name: 'Formulari',

    components:{

        Nom,
        Mobil,
        Codi,
        Mail,
        Psw,
        Confirm,
        ModalBootstrap,
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
