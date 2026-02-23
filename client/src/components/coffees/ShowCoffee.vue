<template>
  <div>
    <h1>Show Coffee</h1>

    <div v-if="coffee">
      <p>id: {{ coffee.id }}</p>

      <!-- ✅ แสดงรูป -->
      <div v-if="coffee.image">
        <img
          :src="`http://localhost:8081/assets/uploads/${coffee.image}`"
          style="width:200px; border-radius:8px; margin-bottom:15px;"
        />
      </div>

      <p>ชื่อเมนู: {{ coffee.name }}</p>
      <p>ราคา: {{ coffee.price }}</p>
      <p>ประเภท: {{ coffee.type }}</p>
      <p>รายละเอียด: {{ coffee.description }}</p>
    </div>

    <div v-else>
      Loading...
    </div>
  </div>
</template>

<script>
import CoffeesService from '../../services/CoffeesService'

export default {
  data () {
    return {
      coffee: null
    }
  },

  async created () {
    const coffeeId = this.$route.params.coffeeId
    this.coffee = (await CoffeesService.show(coffeeId)).data
  }
}
</script>