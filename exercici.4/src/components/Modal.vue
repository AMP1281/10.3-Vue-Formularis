<template>

<div class="modal" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal title</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">

        <p>
            {{nombre}}
            {{mobil}}
            {{codi}}
            {{mail}}
            {{psw}}
            {{confirm}}
        </p>

      </div>

      <div class="modal-footer">
        <button type="button" class="btn btn-primary">Save changes</button>
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>

</template>

<script>
export default {

props:['nombre','mobil','codi','mail','psw','confirm'],



created(){

        this.$root.$on('validar',() => {

            /*
            this.amobil=[];

           if(this.mobil==""){
                this.amobil.push("Aquest camp es obligatori");
           }
           if(this.mobil.length < 6 || this.mobil.length > 13){ 
                this.amobil.push("Aquest camp ha de contenir entre 6 i 13 caràct");
           }
           if(/[0-9]/.test(this.mobil)){ 
                this.amobil.push("El seu nom no pot contenir números.");
           } */

            this.$emit('emobil',this.amobil);

        });

}
}

</script>