<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4"> ISI BUKU KUNJUNGAN</h2>
        <form>
          <div class="mb-3">
            <input type="text" class="form-control form-control-lg rounded-5" placeholder="nama...">
          </div>
          <div class="mb-3">
            <select v-model="form.keanggotaan">
              <option value="">keanggotan</option>
              <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
            </select>
            </div>
            <div class="mb-3">
            <div class="row">
              <div class="col-md-4">
                <select class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">TINGKAT</option>
                  <option value="X">X</option>
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>
                </select>
              </div>
              <div class="col-md-4">
                <select class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                  <option value="TOI">TOI</option>
                </select>
              </div>
              <div class="col-md-4">
                <select class="form-control form-control-lg form-select rounded-5 mb-2">
                  <option value="">KELAS</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
              <select v-model="form.keperluan">
                <option value="">keperluan</option>
                <option v-for="(item, i) in members" :key="i" :value="item.id">{{ item.nama }}</option>
          </div>
          <nuxt-link to="/pengunjung">
          <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kirim</button>
        </nuxt-link>
        <form @submit.prevent="kirimData">
          <input v-model="from.nama" type="text" placeholder="NAMA...">
          <select v-model="from.tingkat"></select>
        </form>
          </form> 
      </div>
    </div>
  </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref ([])

const form = ref ({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
})
const kirimData = async () => {
  const { eror } = await supabase.from('pengunjung').insert([from.value])
  if(!error) navigateTo('/pengunjung')
};
const getKeanggotaan = async () => {
  const{data,error}=await supabase.from('keangotaan').select('*')
  if(data) members.value=data
}

const getKeperluan = async () => {
  const{data,error}=await supabase.from('keangotaan').select('*')
  if(data) members.value=data
}

onMounted(() =>{
  getKeanggotaan
  getKeperluan
})
</script>
