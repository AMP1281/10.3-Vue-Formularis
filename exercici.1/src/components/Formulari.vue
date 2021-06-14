<template>

    <div class="centrar">
        <form @submit.prevent="Validar" novalidate="true">

            <label for="fname">Nom:</label><br>
            <input type="text" id="fname" name="nom" v-model.trim="nom"><br>

            <span v-for="errorn in anom" :key="errorn.id"> {{errorn}} </span><br><br>

            <label for="lmobil">Telèfon mòbil:</label><br>
            <input type="tel" id="lmobil" name="mobil" v-model.trim.number="mobil"><br>

            <span v-for="errorm in amobil" :key="errorm.id"> {{errorm}} </span><br><br>

            <label for="lcodiPostal">Codi Postal:</label><br>
            <input type="text" id="lcodiPostal" name="codiPostal" v-model.trim.number="codiPostal"><br>

            <span v-for="errorc in acodiPostal" :key="errorc.id"> {{errorc}} </span><br><br>

            <label for="lemail">E.mail:</label><br>
            <input type="email" id="lemail" name="email" v-model.trim="email"><br>

            <span v-for="errore in aemail" :key="errore.id"> {{errore}} </span><br><br>

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
       
      
            eobligatori:"Aquest camp es obligatori. ",
            enom:"El seu nom ha de contenir entre 6 i 13 caràcters.",
            enomnumeros:"El seu nom no pot contenir números.",
            enumeros:"Aquest camp nomès pot contenir números.",
            eEmail:"Introdueix una direcció de correu electrónic vàlida.",
       
        
            anom:[],
            amobil:[],
            acodiPostal:[],
            aemail:[],
       
            regExpemail: /[\w._-]+@[\wñ._-]+(?:\.[\w]+)+/,
      }
  },
  methods:{

    Validar(){

            this.anom=[];
                if(!this.nom) {
                    this.anom.push(this.eobligatori);
                } if (this.nom.length < 6 || this.nom.length > 13){
                    this.anom.push(this.enom);
                } if(/[0-9]/.test(this.nom)){
                    this.anom.push(this.enomnumeros);
                }
            this.amobil=[];
                if(!this.mobil) {
                    this.amobil.push(this.eobligatori);
                } else if(isNaN(this.mobil)){
                    this.amobil.push(this.enumeros);
                }

            this.acodiPostal=[];
                if(!this.codiPostal) {
                    this.acodiPostal.push(this.eobligatori);
                } else if(isNaN(this.codiPostal)){
                    this.acodiPostal.push(this.enumeros);
                }
            this.aemail=[];
                if(!this.email) {
                    this.aemail.push(this.eobligatori);
                } else if (!this.regExpemail.test(this.email)) {
                    this.aemail.push(this.eEmail);
                }

    },
  }
};


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
    width: 350px;
}
label{
    color:rgb(112, 112, 112);
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
}
span{
    float:inline-start;
    color: rgb(179, 10, 10);
}


</style>
