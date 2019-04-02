<template>
    <div class="received">
        <div class="bodi-received">
            <div class="img-logo">
                <img src="../assets/images/group.png" class="logoo">
            </div>
            <h1>Masukkan Info Penerima Dana</h1>
            <div class="bodi-input">
                <form>
                    <div class="form-group">
                        <label>Nama Depan Penerima</label>
                        <input type="text" class="form-control">
                    </div>
                    <div class="form-group">
                        <label>Nomor Kartu Identitas</label>
                        <input type="text" class="form-control">
                    </div>
                    <div class="form-group">
                        <label>Nomor Telepon</label>
                        <input type="text" class="form-control">
                    </div>
                    <div class="form-group">
                        <label>Alamat</label>
                        <textarea rows="3" class="form-control"></textarea>
                    </div>
                    <div class="form-group">
                        <button type="submit" data-toggle="modal" data-target="#cekdulu" class="btn btn-cairkan">CAIRKAN DANA</button>
                    </div>
                    <img src="../assets/images/powered_by_kas_pro.png" class="power">
                </form>
            </div>
        </div>
        <div class="modal fade" id="cekdulu" tabindex="-1" role="dialog" aria-labelledby="basicModal" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-body">
              <div class="bodi-sukses">
                 <img src="../assets/images/icon.png" class="img-icon">
                <h2>Pencairan Dana Berhasil!</h2>
                <p>Proses pencairan dana telah berhasil dilakukan, MTCN telah di non-aktifkan. Silakan memberikan dana kepada penerima dengan memberikan struk</p>
              </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-tutup" data-dismiss="modal">OK</button>
            <router-link to="print"><button type="button" class="btn btn-cetak">CETAK STRUK</button></router-link>
          </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
    export default {
        name: 'received',
    }
</script>
