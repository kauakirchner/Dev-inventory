<template>
  <div v-show="autenticado">
    <div class="side-container" v-if="showSidebar">
      <div class="">
        <aside class="">
          <span class="side-title">Dev Inventary</span>
          <hr class="side-hr">
          <div class="menu">
              <span class="side-title">Geral</span>
              <div class="side-item-container">
                <li><router-link class="side-link" to="/inventory">Inventário</router-link></li>
                <li><router-link  @click="logout" class="side-link" to="/">Sair</router-link></li>
              </div>
              <hr>
              <div class="side-item-container">
                <li><span class="side-title">Colaboradores</span></li>
                <li><router-link class="side-link" to="/register-colaborators">Cadastrar</router-link></li>
                <li><router-link class="side-link" to="/colaborators">Ver colaboradores</router-link></li>
              </div>
              <hr>
              <div class="side-item-container">
                <li><span class="side-title">Itens</span></li>
                <li><router-link class="side-link" to="/item-register">Cadastrar</router-link></li>
                <li><router-link class="side-link" to="/item-control">Empréstimo</router-link></li>
              </div>
              <div class="side-show-container">
                <button class="btn btn-outline-primary showSideBar" @click="showSidebar = !showSidebar">⇦</button>
              </div>
          </div>
        </aside>
      </div>
    </div>
    <div v-else>
      <button class="btn btn-primary" @click="showSidebar = !showSidebar">⇨</button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'SideBar',
    data(){
        return{
            showSidebar: true
        }
    },
    methods:{
      logout(){
        this.$store.commit('autenticaLogin/logout')
      }
    },
    computed:{
        autenticado(){
           return this.$store.state.autenticaLogin.autenticado
       }
    },
    mounted(){
      this.$store.state.autenticaLogin.autenticado = localStorage.getItem('loginUsuario') ? true : false
    }
 
}

</script>
<style scoped>

@keyframes fade-in-bar-animation {
  from{
    opacity: 0;
    width: 0%;
    font-size: 5px;
  }
  to{
    opacity: 1;
    width: 100%;
    transition: all 2s;
  }
}

@keyframes fade-out-bar-animation {
  to {
    opacity: 0;
    width: 0%;
    font-size: 5px;
  
  }
  from {
    opacity: 1;
    width: 100%;
    transition: all 2s;
  }
}

li {
  list-style-type: none;
}

.side-container{
    height: 88vh;
    width: 100%;
    justify-content: center;
    align-items: center;
    text-align: center;
    border-right: 1px solid rgba(1, 1, 1, 0.80);
    background-color: #111;
    opacity: .90;
    position: relative;
    animation: fade-in-bar-animation;
    animation-duration: 2s;
}

.side-show-container {
  display: flex;
  justify-content: end;
}

.side-item-container {
  width: 100%;
  margin-top: 15px;
}

.side-title {
  color: #fff;
  font-size: 18px;  

}

.side-link {
  margin-top: 8px;
  font-size: 14px;
  text-shadow: 0px 0px 5px rgb(0, 0, 0, .35);
  padding: 10px 20px;
  color: #fff;
  background-color: transparent;
  font-weight: 500;
  font-size: 14px;
  text-shadow: 0px 0px 5px rgb(0 0 0 / 35%);
  transition: 0.3s ease-in-out;
  display: block;
  text-decoration: none;
  height: 35px;
}
  
.side-link:hover{
  transform: scale(1.025);
  border-bottom: 3px solid #287CD0;
  transition: 0.3s ease-in-out;
  cursor: pointer;
  box-shadow: 0px 0px 10px rgb(0, 0, 0, .5);
  background-color: #111;

}
</style>