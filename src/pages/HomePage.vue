<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        <h1>Gifts:
        </h1>
        <!-- {{ gifts }} -->
      </div>
        <div v-for="gift in gifts" :key="gift.id" class="col-md-3 m-1 gift-card text-shadow">
          <img :src="gift.url" :alt="gift.tag" class="rounded img-fluid" >
          <h3 class="text-dark">{{ gift.title }}</h3>
          <h3 class="text-dark">{{ gift.creatorId }}</h3>
          <h3 class="text-dark">{{ gift.creatorId }}</h3>
          
                  <h3></h3>
        </div>
    </div>
  </div>
</template>

<script>
import { computed, onMounted, onUnmounted } from 'vue';
import { logger } from '../utils/Logger.js';
import Pop from '../utils/Pop.js';
import {giftsService} from '../services/GiftsService.js'
import { AppState } from '../AppState.js';

export default {
  setup() {
async function getGifts(){
  try {
      await giftsService.getGifts();
  } 
    catch (error) {
    Pop.error(error,"GETTING MOVIES")
    
  }
}







    onMounted(()=> {
      logger.log('Mounted?');
      getGifts();

    });

    onUnmounted(() => {
      logger.log('Unmounted?')
    });
        
    
    return {




          gifts: computed(() => AppState.gifts)
        }
  }
}
</script>

<style scoped lang="scss">
.gift-card{
  background-color: rgba(8, 142, 89, 0.507);
    border-radius: 2em;
    border-style: solid;
    box-shadow: 1px 1px 4px black;
    border-width: .2em;
    padding: 1em;
  
}

.text-shadow {
    color: rgb(177, 169, 208);
    text-shadow: 1px 1px 4px black;
}

</style>
