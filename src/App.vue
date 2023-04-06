<script setup>
  import {ref, watch} from 'vue'

  const rate = ref(null)
  const isShine = ref(false)
  const stars = ref(0)
  const halfStar = ref(false)
  const span = ref('')
  const counts = ref(5)
  watch(rate, () => {
    
    isShine.value = true
    stars.value = rate.value
    stars.value = Math.floor(rate.value)

    counts.value = 5 - stars.value

    if(rate.value - stars.value == 0.5){
      counts.value--
      halfStar.value = true

      span.value = '<i class="fa-solid fa-star-half-stroke" class="bright-half" ></i>'
    }
    else {
      halfStar.value = false
    }
  })
</script>

<template>
  <div class="total">
    <div class="input">
      <input type="number" min="1" max="5" step="0.5" v-model="rate">
    </div>
    <div>
      <ul class="shine-stars"  >
        <li>
          <span v-for="star in stars" :key="star" :class="{shine: isShine}">
            <i class="fa-solid fa-star"></i>
          </span>
          <span v-html="span" class="bright-half" v-if="halfStar"></span>
        </li>
        <li>
          <span v-for="count in counts" :key="count">
            <i class="fa-regular fa-star"></i>
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.total{
  border: 1px solid grey;
  border-radius: 15px;
  width: 400px;
  height: 300px;
  padding: 20px;
  margin: 20px
}
*{
  list-style:none;
}
.shine-stars {
  padding: 50px;
  display: flex;
  flex-direction: row;
  width: 200px;

}

input {
  padding: 10px;
  width: 200px;
}

.shine {
  color: yellow;
}

.bright-half {
  color: yellow;
  font-size: 30px;
}
span{
  font-size: 30px;
}



</style>