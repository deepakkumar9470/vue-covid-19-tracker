<template>
  <header class="text-center bg-blue-800 text-white p-4 mb-10">
    <div class="text-2xl md:text-5xl font-bold mb-3">
      <i class="fa fa-viruses"></i>
      Covid-19 Tracker App
    </div>
     <p>
        API by 
        <a class="text-blue-300" href="https://covid19api.com" target="_blank">covid-19api.com</a>
      </p>
  </header>
</template>

<script>
export default {
name :'Header'
}
</script>

<style>
.fa{
  animation: rotate 1s linear infinite;
}

@keyframes rotate {
         0%{
                transform: rotate(0deg);
            }
          
            100%{
                transform: rotate(360deg);
            }    
}
</style>