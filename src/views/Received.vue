<template>
    <div class="received">
        <div class="bodi-received">
            <div class="img-logo">
                <img src="../assets/images/group.png" class="logoo">
            </div>
            <h1>Masukkan Info Penerima Dana</h1>
            <div class="bodi-input">
                <form>
                    <div class="form-inputs">
                        <div class="form-group">
                            <label>Nama Depan Penerima</label>
                            <input type="text" id="nama" v-model="nama" class="form-control">
                        </div>
                        <div class="form-group">
                            <label>Nomor Kartu Identitas</label>
                            <input type="text" id="nomor" :maxlength="maxktp" v-model="nomor" class="form-control">
                        </div>
                        <div class="form-group">
                            <label>Nomor Telepon</label>
                            <input type="text" id="telepon" :maxlength="max" v-model="telepon" class="form-control">
                        </div>
                        <div class="form-group">
                            <label>Alamat</label>
                            <textarea rows="3" id="alamat" v-model="alamat" class="form-control"></textarea>
                        </div>
                        <div class="form-group">
                            <button type="submit" v-on:click="ambildana" v-bind:class="{disabled: isDisabled}" data-toggle="modal" data-target="#cair" class="btn btn-cairkan">CAIRKAN DANA</button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
        <div class="modal fade" id="cair" tabindex="-1" role="dialog" aria-labelledby="basicModal" aria-hidden="true">
      <div class="modal-dialog in">
        <div class="modal-content">
          <div class="modal-body">
              <div class="bodi-sukses" v-if="status == 0">
                 <img src="../assets/images/icon.png" class="img-icon">
                <h2>Pencairan Dana Berhasil!</h2>
                <p>Proses pencairan dana telah berhasil dilakukan, MTCN telah di non-aktifkan. Silakan memberikan dana kepada penerima</p>
              </div>
              <div class="bodi-sukses" v-else-if="status == 1">
                  <img src="../assets/images/remove-icon.png" class="img-icon">
                  <h2>Pencairan Dana Gagal!</h2>
                  <p>Dana telah di ambil oleh Penerima, MTCN telah di non-aktifkan. </p>
              </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-tutup" data-dismiss="modal">OK</button>
            <!-- <router-link to="print"><button type="button" class="btn btn-cetak">CETAK STRUK</button></router-link> -->
          </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
import axios from 'axios'

    export default {
        name: 'received',
        data() {
        return {
        nama: '',
        nomor: '',
        telepon: '',
        alamat: '',
        message: '',
        status: '',
        max: 12,
        maxktp: 16,
        errors: null,
        show: true
        }
    },
    computed: {
    isDisabled() {
        if (this.nama.length > 3 && this.nomor.length > 16  && this.telepon.length > 9 && this.alamat.length > 9 ){
        return false
        }else{
        return true
        }
    }
  },
    methods: {
        ambildana() {
      let app = this
      let id = localStorage.getItem('mtcn')
      axios({
        method: 'post',
        url: 'http://149.129.222.104:8080/receiveMoney/' + id,
        // "Access-Control-Allow-Origin": '*',
         crossdomain: true, 
          "Content-Type": 'application/json'
        }).then(function (response) {
            app.status = response.data.status,
            app.$router.push({ name: 'home'})
        })
        }
    },
    }
</script>
