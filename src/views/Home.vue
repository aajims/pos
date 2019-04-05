
<template>
  <div class="home">
    <div class="input">
      <img src="../assets/images/posfin_logo_white.png" class="img-input">
      <h2>REMITANSI</h2>
      <div class="bodi-home">
         <p>Masukkan 10 digit nomor MTCN</p>
         <input type="text" class="form-controls" :maxlength="max" id="mtcn" v-model="mtcn" placeholder="1234567890" v-int>
          <button data-target="#cekdulu" data-toggle="modal" v-bind:class="{disabled: isDisabled}" v-on:click.prevent="tambahkandata" class="btn btn-cek">CEK NOMOR</button>
      </div>
    </div>
    <div class="modal fade" id="cekdulu" tabindex="-1" role="dialog" aria-labelledby="basicModal" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button> 
            <h4 class="modal-title" id="myModalLabel">Cek Nomor MTCN</h4>
          </div>
          <div class="modal-body" v-if="errorCode == 202"> 
            <tr>
              <td class="nama">Nomor MTCN	</td><td class="sama">:</td><td><b>{{ mtcn }}</b></td>
            </tr>
            <p> Maaf, Dana ini sudah Pernah di Ambil</p>
          </div>
          <div class="modal-body" v-if="errorCode == 203"> 
            <tr>
              <td class="nama">Nomor MTCN	</td><td class="sama">:</td><td><b>{{ mtcn }}</b></td>
            </tr>
            <p> Data MTCN tidak di temukan di Database kami</p>
          </div>
          <div class="modal-body" v-else-if="errorCode == 0">
            <tr>
              <td class="nama">Nomor MTCN	</td><td class="sama">:</td><td><b>{{ mtcn }}</b></td>
            </tr>
            <tr>
              <td class="nama">Tanggal Transaksi	</td><td class="sama">:</td><td><p>{{ insertDate }}</p></td>
            </tr>
            <tr>
              <td class="nama">Nama Pengirim	</td><td class="sama">:</td><td><p>{{ senderName }}</p></td>
            </tr>  
            <tr> 
              <td class="nama">Nama Penerima (sama dengan KTP)	</td><td class="sama">:</td><td><p>{{ receiverName }}</p></td>
            </tr>
            <tr>
              <td class="nama">Nomor HP Penerima	</td><td class="sama">:</td><td><p>{{ receiverPhone }}</p></td>
            </tr>
            <tr>
              <td class="nama">Nilai Dana	</td><td class="sama">:</td><td><b>Rp {{ amount }}</b></td>
            </tr>
          </div>
          <div class="modal-footer" v-if="errorCode == 202">
            <button type="button" class="btn btn-close" data-dismiss="modal">Tutup</button>
          </div>
          <div class="modal-footer" v-if="errorCode == 203">
            <button type="button" class="btn btn-close" data-dismiss="modal">Tutup</button>
          </div>
          <div class="modal-footer" v-else-if="errorCode == 0">
            <button type="button" class="btn btn-close" data-dismiss="modal">Tutup</button>
            <button type="submit" class="btn btn-lanjut" data-dismiss="modal" v-on:click="lanjut">Lanjut Pencairan</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'home',
  data() {
    return {
      mtcn: '',
      status: '',
      insertDate: '',
      senderName: '',
      receiverName: '',
      receiverPhone: '',
      amount: '',
      errorCode: '',
      max: 10,
      errors: null,
      show: true
    }
  },
  computed: {
    isDisabled() {
    if (this.mtcn.length > 9 ){
    return false
    }else{
      return true
    }
    }
  },
  methods: {
    tambahkandata() {
      let app = this
      let id = app.mtcn
      localStorage.setItem('mtcn', id) 
      axios({
        method: 'get',
        url: 'http://149.129.222.104:8080/inquiryMtcn/' + id,
        // "Access-Control-Allow-Origin": '*',
         crossdomain: true, 
          "Content-Type": 'application/json'
        }).then(function (response) {
          if (response.data.mtcn != null) {
            app.mtcn = response.data.mtcn 
            app.insertDate = response.data.insertDate
            app.senderName = response.data.senderName
            app.receiverName = response.data.receiverName
            app.receiverPhone = response.data.receiverPhone
            app.amount = response.data.amount
            app.status = response.data.status
            app.errorCode = 0
          } else {
            app.errorCode = response.data.errorCode
          }
          console.log(response)
      })
    },
    lanjut() {
      this.$router.push('/received')
    }
  },
  created(){
    localStorage.removeItem('mtcn')
  }
}
</script>

