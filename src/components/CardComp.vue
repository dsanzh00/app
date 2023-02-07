<template>
    <div class="card">
        <div class="card-body">
          <h5 v-if="title" class="card-title">{{ title }}</h5>
          <p v-if="parrafo" class="card-text">
            {{ parrafo }}
          </p>
          <slot></slot>
          <div class="d-grid gap-2">
            <button 
                v-for="btn in btns" 
                :key="btn.txt"
                class="btn" 
                :class="btn.class" 
                onclick="location.href='http://localhost:8080/menu'"> 
                {{ btn.txt }}
            </button>
            <slot name="footer"></slot>
          </div>
        </div>
      </div>
</template>

<script>
export default {
    name: 'CardComp',
    props: ['title', 'parrafo', 'btns'],
    methods: {
    iniciarSesion(){
      /*if(this.email.trim() === ''){
        alert('Escribe un correo electrónico');
      }else if(this.password.trim() === ''){
        alert('Escribe un correo electrónico');
      }else{
        var params = {email: this.email.trim(), password: this.password.trim()}
        axios.post('https://app.konfuzio.com/api/v3/auth/', new URLSearchParams({
            'username': 'dsanzh00@estudiantes.unileon.es',
            'password': 'tfg12345'})).then(
              result => {
                var token = result.data.token;
              }
            );
        if(token === 200){
          alert("Correcto")
        }
      }*/

      alert('hola')
    }
  }
        
}


 


</script>

<style scoped>
.card{
    border: none;
    box-shadow: 0 2px 4px black, 0 8px 16px ;
}
</style>