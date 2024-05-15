<script setup>
const supabase = useSupabaseClinet()

const route = useRoute()
const buku = ref(null)

const getBookById = async () => {
  const { data, error } = await supabase.from('buku').select('* kategori(nama)')
    .eq('id', route.params.id)
  if (data) buku.value = data[0]
}

onMounted(() => {
  getBookById()
})
</script>

<template>
  <div v-if="buku" class="container">
    <div class="row mt-3">
      <div class="col-lg-6 pt-5 d-flex justify-content-center">
        <div class="card p-0">
          <div class="card-body p-0">
            <img src="cover1.jpg" width="220px" height="340px" class="cover" alt="cover1">
          </div>
        </div>
      </div>
      <div class="col-lg-6 pt-5 justify-content-center">
        <p>judul : {{ buku.judul }}</p>
        <p>penulis : {{ buku.penulis }}</p>
        <p>kategori : {{ buku.kategori.nama }}</p>
        <p>penerbit : {{ buku.penerbit }}</p>
        <p>tahun : {{ buku.tahun_terbit }}</p>
      </div>
    </div>
    <div class="row mt-5">
      <h2>judul</h2>
      <p class="mt-3">{{ buku.deskripsi }}</p>
    </div>

    <nuxt-link to="/buku">
      <button type="button" class="btn btn-dark mt-5 mb-5">kembali</button>
    </nuxt-link>
  </div>
</template>

<style scoped>
.cover {
  width: 255px;
  height: 370px;
  box-shadow: 1px 10px 50px rgb(0, 0, 0);
}

.card {
  border: none !important;
}

.card-body {
  width: auto;
}
</style>