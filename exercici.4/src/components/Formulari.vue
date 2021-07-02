<template>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form @submit.prevent="validar" novalidate="true" class="w-75 bg-light border border-secondary p-5 rounded">
            
            <Nom :nombre.sync="nombre" label='Nom:' type='text' id='fname' @nombreOk="nOk=$event"/>

            <Mobil :mobil.sync="mobil" label='Telèfon mòbil:' type='text' id='lmobil' @mobilOk="mOk=$event"/>

            <Codi :codi.sync="codi" label='Codi Postal:' type='text' id='lcodiPostal' @codiOk="cpOk=$event"/>

            <Mail :mail.sync="mail" label='E.mail:' type='text' id='lemail' @mailOk="eOk=$event"/>

            <Psw :psw.sync="psw" label='Password:' type='text' id='lpasw' @pswOk="pOk=$event"/>

            <Confirm :confirm.sync="confirm" label='Confirmar Password:' type='text' id='lconfirm' @confirmOk="cOk=$event"/>

        <button type="submit" class="btn btn-primary btn-block mt-5 rounded-pill" :class="{disabled: enableSubmitBtn}" >Validar</button>

        </form>
    

    </div>

        <!-- <form>-->
            <!-- -->
            <!--Nom-->
            <!-- <div class="form-group">
                
                <label for="fname"> Nom: </label>
                
                    <input 
                    class="form-control"
                    type="text"
                    id="fname"
                    name="nom"
                    v-model.trim="nom"  
                    :class="( numero<1 ) ? '': !anom.length ? 'is-valid': 'is-invalid'"
                    autofocus>

                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                        <div class="position-absolute">
                            <small class="text-danger" v-for="(errorn, i) in anom" :key="i"> {{ errorn }} </small>
                        </div>
                    </div>
            </div> -->

             <!--Telèfon mòbil-->
            <!-- <div class="form-group">
                <label for="lmobil" class="mt-3"> Telèfon mòbil: </label>
                <input class="form-control" type="tel" id="lmobil" name="mobil" v-model.trim.number="mobil" :class="( numero<1 ) ? '': !amobil.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <small class="position-absolute text-danger" v-for="(errorm, i) in amobil" :key="i"> {{ errorm }} </small>
                </div>
            </div>
 -->
            <!--Codi Postal-->
            <!-- <div class="form-group">
                <label for="lcodiPostal" class="mt-3"> Codi Postal: </label>
                <input class="form-control" type="text" id="lcodiPostal" name="codiPostal" v-model.trim.number="codiPostal" :class="( numero<1 ) ? '': !acodiPostal.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <small class="position-absolute text-danger" v-for="(errorc, i) in acodiPostal" :key="i"> {{ errorc }} </small>
                </div>
            </div> -->

             <!--e.mail-->
            <!-- <div class="form-group">
                <label for="lemail" class="mt-3"> E.mail: </label>
                <input class="form-control" type="email" id="lemail" name="email" v-model.trim="email" :class="( numero<1 ) ? '': !aemail.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <div class="position-absolute text-danger">
                        <small v-for="(errore, i) in aemail" :key="i"> {{ errore }} </small>
                    </div>
                </div>
            </div> -->

             <!--Password-->
            <!-- <div class="form-row">

                <div class="form-group col-md-6">
                    <label for="lpasw" class="mt-3"> Password: </label>
                    <input class="form-control" type="password" id="lpasw" name="password" v-model.trim="password" :class="( numero<1 ) ? '': !apasw.length ? 'is-valid': 'is-invalid'">
                    <div class="container position-relative col-md-12" style="height: 1em !important;">
                        <div class="position-absolute text-danger">
                            <small v-for="(errorp, i) in apasw" :key="i"> {{ errorp }} </small>
                        </div>
                    </div>
                </div>
 -->
                <!--Confirmar Password-->
                <!-- <div class="form-group col-md-6">
                    <label for="lconfirm" class="mt-3"> Confirmar Password: </label>
                    <input class="form-control" type="password" id="lconfirm" name="confirm" v-model.trim="confirm" :class="( numero<1 ) ? '': !aconfirm.length ? 'is-valid': 'is-invalid'">
                        <div class="container position-relative col-md-12" style="height: 1em !important;">
                            <small class="position-absolute text-danger" v-for="(errorcp, i) in aconfirm" :key="i"> {{ errorcp }} </small>
                        </div>
                    </div>
            </div>

            <input @click="numero++" type="submit" value="Validar" class="btn btn-primary btn-block mt-5 rounded-pill">

                        <Fill id='fname' label='Nom:' type='text' v-model="nombre" name='nNom' @enom="enomp=$event"/> {{enomp}} <p> Value:{{ nombre }} </p>

            <Fill id='lmobil' label='Telèfon mòbil:' type='tel' v-model="mobil" name='nMobil' @emobil="emobilp=$event"/> {{emobilp}}<p> Value:{{ mobil }} </p>

            <Fill id='lcodiPostal' label='Codi Postal:' type='number' v-model="codigoP" name='nCodiP' @ecodi="ecodip=$event"/> {{ecodip}}<p> Value:{{ codigoP }} </p>

            <Fill id='lemail' label='E.mail:' type='email' v-model="mail" name='nMail' @email="emailp=$event"/> {{emailp}} <p> Value:{{ mail }} </p>
            
            <div class="form-row">

                <div class="form-group col-md-6">
                    <Fill id='lpasw' label='Password:' type="password" v-model="contr" name='nPsw' @epasw="epaswp=$event"/> {{epaswp}} <p> Value:{{ contr }} </p>
                </div>

                <div class="form-group col-md-6">
                    <Fill id='lconfirm' label='Confirmar Password:' type="password" v-model="conContra" name='nConPsw' @econfirm="econfirmp=$event"/> {{econfirmp}} <p> Value:{{ conContra }} </p>
                </div>

        </form> -->


</template>

<script>

import Nom from './Nom.vue'
import Mobil from './Mobil.vue'
import Codi from './Codi.vue'
import Mail from './Mail.vue'
import Psw from './Psw.vue'
import Confirm from './Confirm.vue'


export default {
    name: 'Formulari',

    components:{

        Nom,
        Mobil,
        Codi,
        Mail,
        Psw,
        Confirm
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

            isActive: true,
            }
    },
    methods:{
        validar(){

            this.$root.$emit('validar');
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
        }
    },
    
}


</script>

<style>


</style>
