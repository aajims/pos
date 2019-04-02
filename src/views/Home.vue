<template>
  <div class="home">
    <div class="input">
      <img src="../assets/images/posfin_logo_white.png" class="img-input">
      <h2>REMITANSI</h2>
      <div class="bodi-home">
         <p>Masukkan 10 digit nomor MTCN</p>
         <input type="number" class="form-controls" v-model="mtcn" placeholder="1234567890" >
          <a href="#" data-toggle="modal" data-target="#cekdulu" v-on:click.prevent="tambahkandata" class="btn btn-cek">CEK NOMOR</a>
        <img src="../assets/images/powered_by_kas_pro.png" class="power">
      </div>
    </div>
    <div class="modal fade" id="cekdulu" tabindex="-1" role="dialog" aria-labelledby="basicModal" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button> 
            <h4 class="modal-title" id="myModalLabel">Cek Nomor MTCN</h4>
          </div>
          <div class="modal-body">
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
          <div class="modal-footer">
            <button type="button" class="btn btn-close" data-dismiss="modal">Tutup</button>
            <router-link to="received"><button type="button" class="btn btn-lanjut">Lanjut Pencairan</button></router-link>
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
      mtcn: null,
      insertDate: null,
      senderName: null,
      receiverName: null,
      receiverPhone: null,
      amount: null,
      errors: null,
      show: true
    }
  },

    
  methods: {
    tambahkandata() {
      let app = this
      let id = app.mtcn
      axios({
        method: 'get',
        url: 'http://149.129.222.104:8080/inquiryMtcn/' + id,
        // "Access-Control-Allow-Origin": '*',
         crossdomain: true, 
          "Content-Type": 'application/json'
        }).then(function (response) {
          app.mtcn = response.data.mtcn 
          app.insertDate = response.data.insertDate
          app.senderName = response.data.senderName
          app.receiverName = response.data.receiverName
          app.receiverPhone = response.data.receiverPhone
          app.amount = response.data.amount
          console.log(response)
      })
    }

  },

}
</script>

