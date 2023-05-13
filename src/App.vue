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
      //deneme.value = codeUrl._value

    })
    
    .catch((err) => {
      console.log(err)
  })
  }
</script>

<template>
  
  <div class="container-fluid">
    <div class="text-center">
      <img :src="codeUrl">
    </div>

    <div class="form-horizontal">
      <div class="form-group">
        <label class="control-label col-sm-2" for="content">Content:</label>
        <div class="col-sm-10">
          <input type="text"  v-model="dataUrl" class="form-control" id="content" placeholder="Enter content">
        </div>
        <p>{{ dataUrl }}</p>
      </div>
      <div class="form-group"> 
        <div class="col-sm-offset-2 col-sm-10">
          <button type="button" class="btn btn-default" id="generate" @click="getQR()">Generate</button>
        </div>
      </div>
    </div>
  </div>

  



  <RouterView />
</template>

<style scoped>
  #qrcode {
    width: 256px;
    height: 256px;
    margin-top:15px;
  }
</style>
