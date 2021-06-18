<template>

    <div class="container vh-100 d-flex justify-content-center align-items-center align-self-center">

        <form @submit.prevent="Validar" novalidate="true" class="w-75 bg-light border border-secondary p-5 rounded">

            <!--Nom-->
            <div class="form-group">
                <label for="fname"> Nom: </label>
                    <input class="form-control" type="text" id="fname" name="nom" v-model.trim="nom"  :class="( numero<1 ) ? '': !anom.length ? 'is-valid': 'is-invalid'" autofocus>
                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                        <div class="position-absolute">
                            <small class="text-danger" v-for="(errorn, i) in anom" :key="i"> {{ errorn }} </small>
                        </div>
                    </div>
            </div>

             <!--Telèfon mòbil-->
            <div class="form-group">
                <label for="lmobil" class="mt-3"> Telèfon mòbil: </label>
                <input class="form-control" type="tel" id="lmobil" name="mobil" v-model.trim.number="mobil" :class="( numero<1 ) ? '': !amobil.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <small class="position-absolute text-danger" v-for="(errorm, i) in amobil" :key="i"> {{ errorm }} </small>
                </div>
            </div>

            <!--Codi Postal-->
            <div class="form-group">
                <label for="lcodiPostal" class="mt-3"> Codi Postal: </label>
                <input class="form-control" type="text" id="lcodiPostal" name="codiPostal" v-model.trim.number="codiPostal" :class="( numero<1 ) ? '': !acodiPostal.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <small class="position-absolute text-danger" v-for="(errorc, i) in acodiPostal" :key="i"> {{ errorc }} </small>
                </div>
            </div>

             <!--e.mail-->
            <div class="form-group">
                <label for="lemail" class="mt-3"> E.mail: </label>
                <input class="form-control" type="email" id="lemail" name="email" v-model.trim="email" :class="( numero<1 ) ? '': !aemail.length ? 'is-valid': 'is-invalid'">
                <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                    <div class="position-absolute text-danger">
                        <small v-for="(errore, i) in aemail" :key="i"> {{ errore }} </small>
                    </div>
                </div>
            </div>

             <!--Password-->
            <div class="form-row">

                <div class="form-group col-md-6">
                    <label for="lpasw" class="mt-3"> Password: </label>
                    <input class="form-control" type="password" id="lpasw" name="password" v-model.trim="password" :class="( numero<1 ) ? '': !apasw.length ? 'is-valid': 'is-invalid'">
                    <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                        <div class="position-absolute text-danger">
                            <small v-for="(errorp, i) in apasw" :key="i"> {{ errorp }} </small>
                        </div>
                    </div>
                </div>

                <!--Confirmar Password-->
                <div class="form-group col-md-6">
                    <label for="lconfirm" class="mt-3"> Confirmar Password: </label>
                    <input class="form-control" type="password" id="lconfirm" name="confirm" v-model.trim="confirm" :class="( numero<1 ) ? '': !aconfirm.length ? 'is-valid': 'is-invalid'">
                        <div class="container position-relative col-md-12" style="height: 0.9em !important;">
                            <small class="position-absolute text-danger" v-for="(errorcp, i) in aconfirm" :key="i"> {{ errorcp }} </small>
                        </div>
                    </div>
            </div>

            <input @click="numero++" type="submit" value="Validar" class="btn btn-primary btn-block mt-5 rounded-pill">

        </form>

    </div>

</template>

<script>
export default {
  name: 'Formulari',
  data(){

      return{
            numero: 0,

            nom:'',
            mobil:'',
            codiPostal:'',
            email:'',
            password:'',
            confirm:'',
       
            eobligatori:"Aquest camp es obligatori. ",
            enom:"Aquest camp ha de contenir entre 6 i 13 caràcters.",
            enomnumeros:"El seu nom no pot contenir números.",
            enumeros:"Aquest camp nomès pot contenir números.",
            eEmail:"Introdueix una direcció de correu electrónic vàlida.",
            emajus:"Ha de contenir majúscules i minúsvules. ",
            econfirm: "Ha de coincidir amb password. ",
       
            anom:[],
            amobil:[],
            acodiPostal:[],
            aemail:[],
            apasw:[],
            aconfirm:[],
       
            regExpemail: /[\w._-]+@[\wñ._-]+(?:\.[\w]+)+/,

            a:'',
            b:'',
            c:''
      }
  },
  methods:{
    Validar(){

            this.anom=[];
            this.amobil=[];
            this.acodiPostal=[];
            this.aemail=[];
            this.apasw=[];
            this.aconfirm=[];

            this.obligatori(this.nom,this.anom);
            this.obligatori(this.mobil,this.amobil);
            this.obligatori(this.codiPostal,this.acodiPostal);
            this.obligatori(this.email,this.aemail);
            this.obligatori(this.password,this.apasw);
            this.obligatori(this.confirm,this.aconfirm);

            this.minMax(this.nom,this.anom);
            this.minMax(this.password,this.apasw);

            this.mayMin(this.password,this.apasw);

            this.lletres(this.nom,this.anom);

            this.numeros(this.mobil,this.amobil);
            this.numeros(this.codiPostal,this.acodiPostal);

            this.mail(this.email,this.aemail);

            this.igual(this.email,this.confirm, this.aconfirm);

            this.verdadero(this.anom);
            },

            //Validar camps obligatoris
            obligatori(a,b){
                if(!a){
                    b.push(this.eobligatori);
                }
            },
            //Validar min max dígits
            minMax(a,b){ 
                if (a.length < 6 || a.length > 13){ 
                    b.push(this.enom);
                }
            },
            //Validar mayuscules i minuscules obligatories
            mayMin(a,b){
                if (!/[a-z][A-Z]/.test(a)){
                    b.push(this.emajus);
                }
            },
            //Validar que contingui lletres
            lletres(a,b){
                if(/[0-9]/.test(a)){
                    b.push(this.enomnumeros);
                }
            },
            //Validar que contingui números
            numeros(a,b){
                if(isNaN(a)){
                    b.push(this.enumeros);
                }
            },
            //Validar format e.mail
            mail(a,b){
                if (!this.regExpemail.test(a)) {
                    b.push(this.eEmail);
                }
            },
            //Validar que dos inputs siguin identics
            igual(a,b,c){
                if(c != a){
                    b.push(this.econfirm);
                }
            },
  }
}


</script>

<style>


</style>
