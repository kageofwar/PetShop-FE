<template>
    <div class="w-[30vh] sombra_produtos rounded-[4vh] p-4">
        <router-link :to="`/Produtos/${categoria}/${rota}`">
            <div class="flex items-center justify-center">
                <img :src="`${produtoImagem}`" alt="" class="">
            </div>
            <div class="text-[2.2vh]">
                <p>{{ texto }}</p>
            </div>
        </router-link>
        <div class="grid grid-cols-[70%_30%] text-[2.2vh]">
            <router-link :to="`/Produtos/${categoria}/${rota}`">{{ valor }}</router-link>
            <div class="flex transition ease-in-out hover:-translate-y-1 hover:scale-110 duration-300 cursor-pointer">
                <img src="../../../assets/icones/botão carrinho.png" alt="" class="h-12">
            </div>
        </div>
    </div>
</template>

<script>

export default {
    props: [
        'rota',
        'categoria',
        'texto',
        'valor',
        'produtoImagem'
    ]
}


</script>