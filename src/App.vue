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
  
  <div class="main">
    <h1>Generate QRCode for anything</h1>
    <div class="url">
      <div class="textBox">
        <input type="text"  v-model="dataUrl" class="" id="content" placeholder="Enter content">
      </div>
      <div class="generate"> 
        <button type="button" class="" id="generate" @click="getQR()">
          <i class="bi bi-qr-code-scan"></i>
        </button>
      </div>
    </div>
    <div class="qrBox">
      <img :src="codeUrl">
      <a :href="codeUrl" download>
        Download 
        <i class="bi bi-arrow-down-circle-fill"></i>
      </a>
      
    </div>
  </div>
  <RouterView />
</template>

<style scoped lang="scss">
  @import '../public/App.scss'
</style>
