<template>
  <div id="bg">
    <div class="container mt-3">
      <div class="row">
        <div class="col-lg-12 grid-margin stretch-card">
          <div class="card">
            <div class="card-body">
              <p class="card-title float-left"><b>Silahkan cari teman mendakimu di sini</b></p>
              <p class="card-description float-right">
                  <b-button variant="danger" >Logout</b-button>
                </p>
              <div class="table-responsive">
                <b-form-input type="text" v-model="search" v-on:keyup.enter="searching" placeholder="Cari ke gunung mana kamu akan mendaki . . ."></b-form-input>
                <b-table striped hover :items="teman" :fields="fields">
                  <!-- <template v-slot:cell(Aksi)="data">
                    <b-button size="sm" variant="danger" v-on:click="Drop(data.item.id)"><i class="mdi mdi-delete btn-icon-prepend"></i> Hapus</b-button>
                  </template> -->
                </b-table>
                <b-pagination
                  v-model="currentPage"
                  :per-page="perPage"
                  :total-rows="rows"
                  align="center"
                  v-on:input="pagination">
                </b-pagination>

                <p class="card-description" align="center">
                  <b-button variant="primary" v-b-modal.modalTeman v-on:click="Add"><i class="mdi mdi-plus btn-icon-prepend"></i> Upload</b-button>
                </p>

                <b-toast id="loadingToast" title="Processing Data" no-auto-hide>
                  <b-spinner label="Spinning" variant="success"></b-spinner>
                  <strong class="text-success">Loading...</strong>
                </b-toast>

                <!-- toast untuk tampilan message box -->
                <b-toast id="message" title="Message">
                  <strong class="text-success">{{ message }}</strong>
                </b-toast>

              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <b-modal 
      id="modalTeman"
      @ok="Save"
    >
      <template v-slot:modal-title>
        Form Cari Bareng
      </template>
        <form ref="form">
          <div class="form-group">
            <label for="nama" class="col-form-label">Nama</label>
            <input type="text" name="nama" class="form-control" id="nama" placeholder="Nama" v-model="nama">
          </div>
          <div class="form-group">
            <label for="keterangan" class="col-form-label">Keterangan</label>
            <input type="text" name="keterangan" class="form-control" id="keterangan" placeholder="Keterangan" v-model="keterangan">
          </div>
          <div class="form-group">
            <label for="no_hp" class="col-form-label">No Hp</label>
            <input type="text" name="no_hp" class="form-control" id="no_hp" placeholder="No Hp" v-model="no_hp">
          </div>
          <div class="form-group">
            <label for="tujuan" class="col-form-label">Tujuan</label>
            <input type="text" name="tujuan" class="form-control" id="tujuan" placeholder="Nama gunung serta vianya" v-model="tujuan">
          </div>
          <div class="form-group">
            <label for="tanggal_berangkat" class="col-form-label">Tanggal Berangkat</label>
            <input type="date" name="tanggal_berangkat" class="form-control" id="tanggal_berangkat" v-model="tanggal_berangkat">
          </div>
          <div class="form-group">
            <label for="tanggal_pulang" class="col-form-label">Tanggal Pulang</label>
            <input type="date" name="tanggal_pulang" class="form-control" id="tanggal_pulang" v-model="tanggal_pulang">
          </div>
          <div class="form-group">
            <label for="titik_kumpul" class="col-form-label">Titik Kumpul</label>
            <input type="text" name="titik_kumpul" class="form-control" id="titik_kumpul" placeholder="Titik Kumpul" v-model="titik_kumpul">
          </div>
        </form>
    </b-modal>

  </div>
</template>


<script>
module.exports = {
  data : function(){
    return {
      search: "",
      id: "",
      nama: "",
      keterangan: "",
      no_hp: "",
      tujuan: "",
      tanggal_berangkat: "",
      tanggal_pulang: "",
      titik_kumpul: "",
      action: "",
      message: "",
      currentPage: 1,
      rows: 0,
      perPage: 10,
      key: "",
      teman: [],
      fields: [ "tujuan", "tanggal_berangkat", "tanggal_pulang", "titik_kumpul", "nama", "no_hp", "keterangan"],
    }
  },

  methods: {
    searching : function(){
      let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
      let offset = (this.currentPage - 1) * this.perPage;
      this.$bvToast.show("loadingToast");
      let form = new FormData();
      form.append("find", this.search);
      this.axios.post("/teman/" + this.perPage + "/" + offset, form, conf)
      .then(response => {
        if(response.data.status == 1){
          this.$bvToast.hide("loadingToast");
          this.teman = response.data.teman;
          this.rows = response.data.count;
        } else {
          this.$bvToast.hide("loadingToast");
          this.message = "Gagal menampilkan data ."
          this.$bvToast.show("message");
          // this.$router.push({name: "login"})
        }
      })
      .catch(error => {
          console.log(error);
      });
    },

    getData : function(){
      let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
      let offset = (this.currentPage - 1) * this.perPage;
      this.$bvToast.show("loadingToast");
      this.axios.get("/teman/" + this.perPage + "/" + offset, conf)
      .then(response => {
        if(response.data.status == 1){
          this.$bvToast.hide("loadingToast");
          this.teman = response.data.teman;
          this.rows = response.data.count;
        } else {
          this.$bvToast.hide("loadingToast");
          this.message = "Gagal menampilkan data"
          this.$bvToast.show("message");
          // this.$router.push({name: "login"})
        }
        
      })
      .catch(error => {
        console.log(error);
      });
    },

    pagination : function(){
      if(this.search == ""){
        this.getData();
      } else {
        this.searching();
      }
    },

    Add : function(){
      this.action = "insert";
      this.nama = "";
      this.keterangan = "";
      this.no_hp = ""; 
      this.tujuan = "";
      this.tanggal_berangkat = "";
      this.tanggal_pulang = ""; 
      this.titik_kumpul = "";
    },

    Save : function(){
      let conf = { headers: { "Authorization" : 'Bearer ' + this.key } };
      this.$bvToast.show("loadingToast");
      if(this.action === "insert"){
        let form = new FormData();
        form.append("id", this.id);
        form.append("nama", this.nama);
        form.append("keterangan", this.keterangan);
        form.append("no_hp", this.no_hp);
        form.append("tujuan", this.tujuan);
        form.append("tanggal_berangkat", this.tanggal_berangkat);
        form.append("tanggal_pulang", this.tanggal_pulang);
        form.append("titik_kumpul", this.titik_kumpul);

        this.axios.post("/teman", form, conf)
        .then(response => {
          this.$bvToast.hide("loadingToast");
          if(this.search == ""){
            this.getData();
          } else {
            this.searching();
          }
          this.message = response.data.message;
          this.$bvToast.show("message");
        })
        .catch(error => {
          console.log(error);
        });
      }
    },

    Drop : function(id){
      let conf = { headers: { "Authorization" : "Bearer " + this.key} };
      if(confirm('Apakah anda yakin ingin menghapus data ini?')){
        this.$bvToast.show("loadingToast");
        this.axios.delete("/teman/" + id, conf)
        .then(response => {
            this.getData();
            this.$bvToast.hide("loadingToast");
            this.message = response.data.message;
            this.$bvToast.show("message");
        })
        .catch(error => {
          console.log(error);
        });
      }
    },

    logout:function(){
          let conf = { headers : {"Authorization" : "Bearer " + localStorage.getItem("Authorization")} };
          let form = new FormData();
          this.axios.post('/logout', form, conf).then(response => {
            if (response.data.logged === false || response.data.status === 0) {
                this.$store.commit('logout')
                localStorage.removeItem("Authorization")
                this.$router.push({name: 'login'})
            }
          }).catch(error => {

        });
      },
  },
  mounted(){
    this.key = localStorage.getItem("Authorization");
    this.getData();
  }
}
</script>