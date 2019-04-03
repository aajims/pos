<template>
    <div class="logins">
        <div class="full-bodi">
            <div class="bodi-login">
                <div class="login">
                    <img src="../assets/images/posfin_logo_color.png" class="img-login">
                    <h2>Remitansi</h2>
                    <div class="alert alert-danger" v-for="error in errors">
                        <p>{{ error }}</p>
                    </div>
                    <form role="form" @submit.prevent="login">
                        <div class="form-group">
                            <input type="text" name="username" class="form-control" v-model="username" placeholder="Username">
                        </div>
                        <div class="form-group">
                            <input type="password" name="password" class="form-control" v-model="password" placeholder="Password">
                        </div>
                        <p>Lupa Password?</p>
                        <button type="submit" class="btn btn-login">LOGIN</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'logins',
        data: function () {
        return {
        username: null,
        password: null,
        sukses: null,
        errors: null
        }
    },
    methods: {
        login() {
            this.errors = []
            if (this.username == null ) {
                this.errors.push('Username Harus di isi !')
                return false
            } else if (this.password == null ) {
                this.errors.push('Password harus di isi !')
                return false
            }
            var app = this
            app.$router.push('/home')
        }
        
    }
    }
</script>
