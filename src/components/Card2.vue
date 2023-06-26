<script setup>

    import { computed, ref, onUnmounted} from 'vue';

    defineProps({
        src: String
    });

    const detalles = ref(false);

    const labelBoton = computed(()=>{
        return detalles.value ? 'Ocultar detalles' : 'Ver detalles';
    })

    onUnmounted(()=>{
        console.log('destruyendo componente')
    })

</script>
    
<template>

    <keep-alive>
        <div class="container">
            <img :src="src" alt="imagen de comida de pixabay">
            <div class="info">            
                <div class="title">
                    <slot name="title"></slot>
                </div>
                <div class="actions">
                    <button @click="detalles=!detalles">{{ labelBoton }}</button>
                </div>
                <div class="content" v-if="detalles">
                    <slot name="description"></slot>
                </div>  
                <slot></slot>          
            </div>
        </div>

    </keep-alive>


    
    
</template>

<style scoped>
    .container{
        max-width: 150px;
        border: 1px solid #b80d0d;
    }

    img{
        max-width: 150px;
    }

    .info{
        padding: 5px;
    }

    .title h2{
        color: coral;
        text-align: left;
        font-size: 10px;
    }

    .content{
        text-align: justify;
    }

    button{
        margin: 10px 0;
        padding: 5px;
    }

</style>