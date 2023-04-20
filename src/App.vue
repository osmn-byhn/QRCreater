<script setup>
  import { RouterLink, RouterView } from 'vue-router'
  import { reactive } from 'vue'

  function htmlEncode (value){
  return $('<div/>').text(value).html();
}

$(function() {
  $("#generate").click(function() {
    $(".qr-code").attr("src", "https://chart.googleapis.com/chart?cht=qr&chl=" + htmlEncode($("#content").val()) + "&chs=160x160&chld=L|0");
  });
});
</script>

<template>
  
  <div class="container-fluid">
  <div class="text-center">
    <img src="https://chart.googleapis.com/chart?cht=qr&chl=Hello+World&chs=160x160&chld=L|0"
         class="qr-code img-thumbnail img-responsive">
  </div>

  <div class="form-horizontal">
    <div class="form-group">
      <label class="control-label col-sm-2" for="content">Content:</label>
      <div class="col-sm-10">
        <input type="text" class="form-control" id="content" placeholder="Enter content">
      </div>
    </div>
    <div class="form-group"> 
      <div class="col-sm-offset-2 col-sm-10">
        <button type="button" class="btn btn-default" id="generate">Generate</button>
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
