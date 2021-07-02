<template>

    <div class="form-group">
        
        <label :for="id"> {{ label }} </label>
        
        <input
        class= 'form-control'
        :id= 'id'
        :name= 'name'
        :type= 'type'
        :value='value'
        @input='$emit("input", $event.target.value)'
        />

    </div>






    <!--     :class="( numero<1 ) ? '': !anom.length ? 'is-valid': 'is-invalid'"
    autofocus>

    <div class="container position-relative col-md-12" style="height: 0.9em !important;">
        <div class="position-absolute">
            <small class="text-danger" v-for="(errorn, i) in anom" :key="i"> {{ errorn }} </small>
        </div>
    </div>


    > -->





</template>

<script>
export default {
    props:{
        id:{
            type: String,
            required: true,
        },
        label:{
            type: String,
            required:true,
        },
        name:{
            type:String,
            required:true,
        },
        type:{
            type:String,
            required:true,
        },
        value:{
            type: [String, Number],
            required: true,
        },
        
    },

    data(){
        return{

            anom:[],
            amobil:[],
            acodiPostal:[],
            aemail:[],
            apasw:[],
            aconfirm:[],

        }
    },

    computed:{
        actualizar:{
            get(){
                return this.value
            }
        }
    },

    

    created(){

        this.anom=[];

        this.$root.$on('validar',() => {

           if(this.value==""){
                this.anom.push("Aquest camp es obligatori");
           }
           if(this.$props.value.length < 6 || this.$props.value.length > 13){ 
                this.anom.push("Aquest camp ha de contenir entre 6 i 13 caràct");
           }

            this.$emit('enom',this.anom.toString())
        });
    }
}

   

    
    



    //data(){
    //    return{
    //        errors:[],
    //    }
    //},

    //methods:{

        //errors:[],

        //obligatori(){
        //    if(!this.value){
        //        errors.push("Aquest camp es obligatori")
        //}
    //}
    //}





/*
      data(){
/*
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
/*
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
            }, */
</script>



