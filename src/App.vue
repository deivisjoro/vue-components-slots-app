<script setup>
  import { ref, shallowRef, computed } from 'vue';
  import Card from './components/Card.vue';
  import Card2 from './components/Card2.vue';

  const productos = [
    {
      title: 'Espárragos',
      description: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, obcaecati recusandae hic sint repudiandae porro, maxime reiciendis officiis voluptas nisi et nostrum illo, dolorum rem doloribus vel non libero rerum.',
      image: 'https://cdn.pixabay.com/photo/2017/03/23/19/57/asparagus-2169305_1280.jpg'
    },
    {
      title: 'Carne, Comida y Proteína',
      description: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, obcaecati recusandae hic sint repudiandae porro, maxime reiciendis officiis voluptas nisi et nostrum illo, dolorum rem doloribus vel non libero rerum.',
      image: 'https://cdn.pixabay.com/photo/2016/01/22/02/13/meat-1155132_1280.jpg'
    },
    {
      title: 'Carne de res, Papas fritas y Dieta',
      description: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, obcaecati recusandae hic sint repudiandae porro, maxime reiciendis officiis voluptas nisi et nostrum illo, dolorum rem doloribus vel non libero rerum.',
      image: 'https://cdn.pixabay.com/photo/2012/03/02/00/29/beef-20678_1280.jpg'
    },
    {
      title: 'Carne de res, Comida y Verde',
      description: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, obcaecati recusandae hic sint repudiandae porro, maxime reiciendis officiis voluptas nisi et nostrum illo, dolorum rem doloribus vel non libero rerum.',
      image: 'https://cdn.pixabay.com/photo/2016/03/05/22/08/beef-1239187_1280.jpg'
    },
    {
      title: 'Panqueques, Crepes y Lleno',
      description: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, obcaecati recusandae hic sint repudiandae porro, maxime reiciendis officiis voluptas nisi et nostrum illo, dolorum rem doloribus vel non libero rerum.',
      image: 'https://cdn.pixabay.com/photo/2014/12/22/16/50/pancake-577386_1280.jpg'
    },
  ];

  const myComponent = shallowRef(Card);

  const fnChangeComponent = () => {
    if(myComponent.value===Card){
      myComponent.value = Card2;
    }
    else{
      myComponent.value = Card;
    }
  }

  
  const labelBoton = computed(()=>{
      return (myComponent.value === Card) ? 'Pequeño' : 'Grande';
  })


</script>

<template>
  <main>
    <h1>Comidas</h1>
    <!--componentes dinamicos -->
    <div>    
      <button @click="fnChangeComponent">Cambiar componente ({{ labelBoton }})</button>
    </div>    
    <div class="content">
      <component :is="myComponent" v-for="(producto, index) in productos" :key="index" :src="producto.image">
        <template v-slot:title>
          <h2>{{ producto.title }}</h2>
        </template>
        <template v-slot:description>
          <p>{{ producto.description }}</p>
        </template>
        <p class="pie">pie de la tarjeta</p>
      </component>
    </div>
    <hr>
    <!-- se llama directamente al componente -->  
    <div class="content">
      <Card v-for="(producto, index) in productos" :key="index" :src="producto.image">
        <template v-slot:title>
          <h2>{{ producto.title }}</h2>
        </template>
        <template v-slot:description>
          <p>{{ producto.description }}</p>
        </template>
        <p class="pie">pie de la tarjeta</p>
      </Card>      
    </div>
  </main>
</template>

<style scoped>

h1{
  text-align: center;
  padding: 10px;
}

.content{
  margin-top: 35px;
  display: flex;
  flex-wrap: wrap;
  gap: 25px;
}

main{
  padding: 20px;
}

h2{
  text-align: center;
  color: darkslateblue;
  padding: 10px;
  font-size: 20px; 
  font-weight: bold;
}

.pie{
  text-align: right;
  font-size: 12px;
}
</style>
