<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter...">
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table table-bordered">
          <thead>
            <tr> 
              <td>#</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>KELAS</td>
              <td>JURUSAN</td>
              <td>TINGKAT</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1.</td>  
              <td>Dini Oktapriyanti</td>  
              <td>Siswa</td> 
              <td>XI</td>
              <td>PPLG</td>
              <td>1</td> 
              <td>24 Febuary 2024, 23.31.00</td>  
              <td>Baca</td>  
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <nuxt-link to="/pengunjung/tambah">
    <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">Kembali</button>
    </nuxt-link>
  </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getpengunjung = async () => {
  const{data,error}=await supabase.from('pengunjung').select('*), keanggotaan(*),keperluan(*)')
  if(data) visitors.value=data
}

onMounted(() => {
  getpengunjung()
})
</script>
