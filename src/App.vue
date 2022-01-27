<template>
<Header />
<div class="container">
  <router-view/>
</div>
  
</template>

<script>
//objeto de componentes call...
import Header from '@/components/Header'


export default{
  components:{
    Header,
  },
}
</script>


