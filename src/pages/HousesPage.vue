<template>
<div v-for="h in houses" :key="h.id">

</div>



</template>



<script>
import { computed } from '@vue/reactivity'
import { onMounted } from 'vue'
import { AppState } from '../AppState.js'
import { housesService } from '../services/HousesService.js'
import { logger } from '../utils/Logger.js'
import Pop from '../utils/Pop.js'

export default {
setup() {
  
  async function getHouses(){
    try {
    await housesService.getHouses()  
    } catch (error) {
    logger.error('[Getting Houses]',error)
    Pop.error(error) 
    }
  }
  

  onMounted(()=> {
    getHouses()
    })
  return {
  houses: computed(()=> AppState.houses)
  }
}
}





</script>
<style>
</style>