<template>
    <div class="container">
        <div class="col-md-12">
            <div class="card">
                <div class="card-body">
                    <h2> Form Data Komplek Panghegar</h2>
                    
                    <form style="text-align:left" @submit.prevent="handleSubmit" id="formdata">
                        <div class="form-group row">
                            <label for="staticNama" class="col-sm-2 col-form-label"></label>
                            <div class="col-sm-10">
                                <p v-if="data.errors.length">
                                    <b>Mohon perbaiki kesalahan-kesalahan berikut:</b>
                                    <ul>
                                        <li v-for="error in data.errors" :key="error" style="color:red">{{ error }}</li>
                                    </ul>
                                </p>
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticNama" class="col-sm-2 col-form-label"><b>Nama</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" placeholder="Nama..." v-model="data.nama">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticNik" class="col-sm-2 col-form-label"><b>NIK</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" placeholder="NIK..." v-model="data.nik">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticNkk" class="col-sm-2 col-form-label"><b>Nomor Kartu Keluarga</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" placeholder="Nomor Kartu Keluarga..." v-model="data.kk">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticFotoktp" class="col-sm-2 col-form-label"><b>Foto KTP</b></label>
                            <div class="col-sm-10">
                                <input type="file" class="form-control-file" ref="file" @change="changeKTP" accept="image/x-png,image/gif,image/jpeg,image/jpg">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticFotokk" class="col-sm-2 col-form-label"><b>Foto Kartu Keluarga</b></label>
                            <div class="col-sm-10">
                                <input type="file" class="form-control-file" ref="file_kk" @change="changeKK" accept="image/x-png,image/gif,image/jpeg,image/jpg">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticFotokk" class="col-sm-2 col-form-label"><b>Umur</b></label>
                            <div class="col-sm-10">
                                <input type="number" class="form-control" v-model="data.umur" placeholder="Umur...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticJk" class="col-sm-2 col-form-label"><b>Jenis Kelamin</b></label>
                            <div class="col-sm-10">
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" id="1" value="1" v-model="data.jk" />
                                    <label class="form-check-label" for="inlineLaki">Laki - laki</label>
                                </div>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" id="2" value="2" v-model="data.jk" />
                                    <label class="form-check-label" for="inlinePerempuan">Perempuan</label>
                                </div>
                            </div>
                            
                        </div>
                        <div class="form-group row">
                            <label for="staticAlamat" class="col-sm-2 col-form-label"><b>Alamat</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" v-model="data.alamat" placeholder="Alamat...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticRt" class="col-sm-2 col-form-label"><b>RT</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" v-model="data.rt" placeholder="RT...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticRw" class="col-sm-2 col-form-label"><b>RW</b></label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" v-model="data.rw" placeholder="RW...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticPenghasilanBefore" class="col-sm-2 col-form-label"><b>Penghasilan sebelum pandemi</b></label>
                            <div class="col-sm-10">
                                <input type="number" class="form-control" v-model="data.income_before" placeholder="Penghasilan sebelum pandemi...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticPenghasilanAfter" class="col-sm-2 col-form-label"><b>Penghasilan setelah pandemi</b></label>
                            <div class="col-sm-10">
                                <input type="number" class="form-control" v-model="data.income_after" placeholder="Penghasilan setelah pandemi...">
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="staticAlasanLain" class="col-sm-2 col-form-label"><b>Alasan membutuhkan bantuan</b></label>
                            <div class="col-sm-10">
                                <select class="form-control"  @change="onChangeAlasan($event)" data-placeholder="Alasan" v-model="data.alasan">
                                    <option value="0"> - Pilih Alasan - </option>
                                    <option value="Kehilangan Pekerjaan">Kehilangan Pekerjaan</option>
                                    <option value="Kepala Keluarga terdampak atau korban Covid">Kepala Keluarga terdampak atau korban Covid</option>
                                    <option value="Tergolong fakir/miskin semenjak sebelum Covid">Tergolong fakir/miskin semenjak sebelum Covid</option>
                                    <option value="Lainnya">Lainnya....</option>
                                </select>
                                <br>
                                <input type="text" class="form-control" v-model="data.alasan_lain" placeholder="Alasan lain..." v-if="showAlasan">
                            </div>
                        </div>
                        <div class="form-group row">
                            <div class="col-md-12">
                                <input type="checkbox" v-model="data.terms" required />
                                Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.
                            </div>
                        </div>
                        <div class="form-group row">
                            <label for="static" class="col-sm-2 col-form-label"></label>
                            <div class="col-md-10">
                                <button class="btn btn-primary" > Submit </button>
                            </div>
                        </div>
                    </form>
                  
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            data : {
                nama    : '',
                nik     : '',
                foto_ktp: '',
                foto_kk : '',
                kk      : '',
                umur    : '',
                jk      : '',
                alamat  : '',
                rt      : '',
                rw      : '',
                income_before : '',
                income_after  : '',
                alasan  : '0',
                alasan_lain  : '',
                terms   : false,
                errors : []
            },
            showAlasan : false
        }
    },
    methods: {
        handleSubmit(){
            this.data.errors = [];
            if(!this.data.nama) this.data.errors.push("Nama harus diisi");
            if(!this.data.nik) this.data.errors.push("NIK harus diisi");
            if(!this.data.kk) this.data.errors.push("Nomor Kartu Keluarga harus diisi");
            if(!this.data.umur) this.data.errors.push("Umur harus diisi");
            if(!this.data.jk) this.data.errors.push("Jenis Kelamin harus diisi");
            if(!this.data.alamat) this.data.errors.push("Alamat harus diisi");
            if(this.data.alamat.length >= 255) this.data.errors.push("Alamat maksimal 255");
            if(!this.data.income_before) this.data.errors.push("Penghasilan sebelum pandemi harus diisi");
            if(!this.data.income_after) this.data.errors.push("Penghasilan setelah pandemi harus diisi");
            if(!this.data.alasan) this.data.errors.push("Alasan harus diisi");
            if(this.data.umur < 25) this.data.errors.push("Umur lebih dari atau sama dengan 25 tahun");

            const fileKTP = this.$refs.file.files[0];
            const fileKK = this.$refs.file_kk.files[0];
            
            if (!fileKTP) {
                this.data.errors.push("File KTP harus diisi");
            }
            if (fileKTP) {
                if(fileKTP.size > 2_097_152){
                    this.data.errors.push("File KTP Maximal 2MB");
                }
                if(fileKTP['type'] !== 'image/jpeg' && fileKTP['type'] !== 'image/jpg' && 
                fileKTP['type'] !== 'image/gif' && fileKTP['type'] !== 'image/png'
                ){
                    this.data.errors.push("File KTP harus jpeg/png/gif/png");
                }
            }
            
           
            
            if (!fileKK) {
                this.data.errors.push("File Kartu Keluarga harus diisi");
            }
            if(fileKK){
                if (fileKK.size > 2_097_152) {
                    this.data.errors.push("File Kartu Keluarga Maximal 2MB");
                }
                if(fileKK['type'] !== 'image/jpeg' && fileKK['type'] !== 'image/jpg' && 
                    fileKK['type'] !== 'image/gif' && fileKK['type'] !== 'image/png'
                ){
                    this.data.errors.push("File KTP harus jpeg/png/gif/png");
                }
            }
           

            if(this.data.errors.length > 0){
                alert('Submit Failed');
                return false;
            }
            if(!this.data.errors.length){
                try {
                    console.log(this.data);
                    console.log(Math.random());
                    alert('Submit Success');
                } catch(e) {
                    console.log('Exception: ', e)
                }

            }
        },
        onChangeAlasan(e){
            const idAlasan = e.target.value;
            if(idAlasan == 'Lainnya'){
                this.showAlasan = true;            
            }else{
                this.showAlasan = false;
            }
        },
        changeKTP(){
            this.data.foto_ktp = this.files = this.$refs.file.files[0].name;
        },
        changeKK(){
            this.data.foto_kk = this.files = this.$refs.file_kk.files[0].name;
        }
    }
}
</script>