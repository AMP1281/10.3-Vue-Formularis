<template>

    <div class="centrar">

        <form @submit.prevent="Validar" novalidate="true">

            <!--Nom-->
            <label for="fname">Nom:</label><br>
            <input type="text" id="fname" name="nom" v-model.trim="nom"><br>

            <span v-for="errorn in anom" :key="errorn.id"> {{errorn}} </span><br><br>

             <!--Telèfon mòbil-->
            <label for="lmobil">Telèfon mòbil:</label><br>
            <input type="tel" id="lmobil" name="mobil" v-model.trim.number="mobil"><br>

            <span v-for="errorm in amobil" :key="errorm.id"> {{errorm}} </span><br><br>

            <!--Codi Postal-->
            <label for="lcodiPostal">Codi Postal:</label><br>
            <input type="text" id="lcodiPostal" name="codiPostal" v-model.trim.number="codiPostal"><br>

            <span v-for="errorc in acodiPostal" :key="errorc.id"> {{errorc}} </span><br><br>

             <!--e.mail-->
            <label for="lemail">E.mail:</label><br>
            <input type="email" id="lemail" name="email" v-model.trim="email"><br>

            <span v-for="errore in aemail" :key="errore.id"> {{errore}} </span><br><br>

             <!--Password-->
            <label for="lpasw">Password:</label><br>
            <input type="text" id="lpasw" name="password" v-model.trim="password"><br>

            <span v-for="errorp in apasw" :key="errorp.id"> {{errorp}} </span><br><br>

             <!--Confirmar Password-->
            <label for="lconfirm">Confirmar Password:</label><br>
            <input type="text" id="lconfirm" name="confirm" v-model.trim="confirm"><br>

            <span v-for="errorcp in aconfirm" :key="errorcp.id"> {{errorcp}} </span><br><br>

            <input type="submit" value="Validar" class="boton"><br><br>

        </form>

    </div>

</template>

<script>
export default {
  name: 'Formulari',
  data(){
      return{
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
            c:'',
      }
  },
  methods:{
    Validar(){

            this.anom=[];
            this.amobil=[],
            this.acodiPostal=[],
            this.aemail=[],
            this.apasw=[],
            this.aconfirm=[],

            this.obligatori(this.nom,this.anom);
            this.obligatori(this.mobil,this.amobil);
            this.obligatori(this.codiPostal,this.acodiPostal);
            this.obligatori(this.email,this.aemail);
            this.obligatori(this.pasw,this.apasw);
            this.obligatori(this.confirm,this.aconfirm);

            this.minMax(this.nom,this.anom);
            this.minMax(this.password,this.apasw);

            this.mayMin(this.password,this.apasw);

            this.lletres(this.nom,this.anom);

            this.numeros(this.mobil,this.amobil);
            this.numeros(this.codiPostal,this.acodiPostal);

            this.mail(this.email,this.aemail);

            this.igual(this.email,this.confirm, this.aconfirm)
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
html, body, div, span, applet, object, iframe,h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,b, u, i, center,
dl, dt, dd, ol, ul, li,fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,menu, nav, output, ruby, section, summary,
time, mark, audio, video 
{
    margin: 0;
    padding: 0;
    border: 0;
    font: inherit;
    font-size: 100%;
    vertical-align: baseline;
}
*{box-sizing: border-box;
}
body{
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;
    background:-moz-linear-gradient(50deg,#cffffe,#1687a7);
    font-family:Arial, Helvetica, sans-serif;
}
.centrar{
    height: 100%;
    width: 100%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;
    background-color:#f6f5f5;
    padding: 40px;
    border-radius: 3px;
    box-shadow:2px 2px 10px 2px rgba(65, 64, 64, 0.533);
}
form{
    width: 550px;
}
label{
    color:rgb(112, 112, 112);
    font-weight: bold;
}
input{
    outline:none;
    border-radius: 3px;
    border: solid 1px rgba(153, 153, 153, 0.952);
    padding: 0.5em;
    width:100%;
    margin-top:1.5%;
}
input:focus{
    border-color:#39A9CB;
}
.boton{
    background:#39A9CB;
    border:none;
    color:white;
    padding:0.7em;
    letter-spacing: 0.10em;
    font-size:1em;
    font-weight: bold;
}
span{
   float:inline-start;
   color: rgb(179, 10, 10);
}


</style>
