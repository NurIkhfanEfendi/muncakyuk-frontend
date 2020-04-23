<template>
  <div>
        <div>
            <br>
            <article class="card-body mx-auto" style="max-width: 400px;">
                <img src="../../public/img/mount-logo.png" width="30%" height="30%" style="display: block; margin: auto;">
                <h4 class="card-title mt-3 text-center note">Silahkan Daftar</h4>
                <p class="text-center">Daftarkan diri anda terlebih dahulu.</p>
                <br>
                <form v-on:submit.prevent="Register">
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-user"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Nama Depan" type="text" v-model="firstname">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-user"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Nama Belakang" type="text" v-model="lastname">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-envelope"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Alamat Email" type="email" v-model="email">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Password" type="password" v-model="password">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Konfirmasi Password" type="password" v-model="password_verify">
                    </div>
                    <div class="form-group">
                        <button type="submit" href="#pablo" class="btn btn-primary btn-block"> Daftar </button>
                    </div>
                </form>
            </article>
        </div>
    </div>
</template>

<script>
export default {
    data() {
      return {
        firstname: '',
        lastname: '',
        email: '',
        password: '',
        password_verify: ''
      }
    },
    methods: {
        Register: function(){
            let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
            this.$bvToast.show("loadingToast");
            let form = new FormData();
            form.append("id", this.id);
            form.append("firstname", this.firstname);
            form.append("lastname", this.lastname);
            form.append("email", this.email);
            form.append("password", this.password);
            form.append("password_verify", this.password_verify);

            this.axios.post("/register", form, conf)
            .then(() => this.$router.push('/login'))
            .catch(error => {
              console.log(error);
            }); 
        }
    }
}
</script>
