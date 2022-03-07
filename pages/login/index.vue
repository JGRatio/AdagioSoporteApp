<template>
   
        <!-- CONTENEDOR PRINCIPAL -->
        <div class="row mb-0">
        <!-- FORM LOGIN -->
        <div class="text-center mt-5 mx-5 col" cz-shortcut-listen="true">
        <form class="form-signin mx-5">
        <img class="mb-4" src="@/src/images/logo.jpg" alt="" width="150" height="150">
        <h1 class="">¡Hola bienvenido!</h1>
        <p><em>Inicia Sesión para comenzar</em></p>
        <div class="mx-5">
            <!-- <label for="inputEmail" class="sr-only">Email address</label> -->
            <input id="inputEmail" type="email" class="form-control" placeholder="Email address" required="" autofocus="">
            <!-- <label for="inputPassword" class="sr-only">Password</label> -->
            <input id="inputPassword" type="password" class="form-control mt-2" placeholder="Password" required="">
            <div class="checkbox mb-3 mt-3">
                <label>
                <input type="checkbox" value="remember-me"> Recuérdame
                </label>
            </div>
        </div>
        <div class="row">
            <div class="col"></div>
            <button class="btn btn-lg btn-primary btn-block col" type="submit">Acceder</button>
            <div class="col"></div>
        </div>
        
        <p class="mt-5 mb-3 text-muted">© 2022</p>
        </form>
       
        </div>
         <!-- IMAGEN LADO IZQUIERDO -->
         <div class="col">
            <img src="@/src/images/loginBackground.jpg" class="img-fluid" alt="Responsive image" style="height:602px" >
        </div>
        </div>
    
  

</template>

<script>
    export default {
        name:'PxComponent'
    }
</script>

<style lang="scss" scoped>

</style>