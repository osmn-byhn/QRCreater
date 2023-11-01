<script setup>
  import { RouterLink, RouterView } from 'vue-router'
  import { reactive, ref } from 'vue'
  import axios from 'axios'
  const codeUrl = ref('')
  const dataUrl = ref('')

  const config = {
    headers: {
      'X-Api-Key': '0IM1OGs36No1KIg69Tg75G4IiT5UvWVe8UrDaRnI'
    }
  }
  var fmt = 'png'
  function getQR() {
    axios.get(`https://api.api-ninjas.com/v1/qrcode?data=${dataUrl._value}&format=${fmt}&size=200`, config)
    .then((res) => {
      console.log(dataUrl);
      console.log(res.data)
      codeUrl.value = `data:image/png;base64, ${res.data}`

    })
    
    .catch((err) => {
      console.log(err)
  })
  }
   VanillaTilt.init(document.querySelectorAll(".main"), {
		max: 25,
        speed: 400,
        easing:"cubic-bezier(.03,.98,.52,.99)",
        perspective:500,
        transition:true
    });
</script>

<template>
  
  <div class="main container">
    <h1>Generate QRCode for anything</h1>
    <br>
    <div class="input-group mb-3">
      <input type="text" v-model="dataUrl" class="form-control" placeholder="Recipient's username" aria-label="Recipient's username" aria-describedby="button-addon2">
      <button type="button" class="btn btn-primary" id="generate" @click="getQR()">
          <i class="bi bi-qr-code-scan"></i>
        </button>
    </div>

    
    <div class="qrBox">
      <img :src="codeUrl">
     
    </div>
    <br>
    <a :href="codeUrl" download class=" btn btn-success col-12">
        Download 
        <i class="bi bi-arrow-down-circle-fill"></i>
      </a>
  </div>
</template>

<style scoped lang="scss">
  @import '../public/App.scss'
</style>
