<template>
    <div class="bg-[--azul-claro]">

        <headerPrincipal />
        <headerCategoria />

        <img src="../assets/onda-branca-bottom.png" alt="" class="-translate-y-[79px]">
        <div class="grid grid-cols-2 -translate-y-10">
            <div class="flex justify-center items-center flex-col text-[3.2vh] font-bold text-white">
                <h2>Todos os Produtos</h2>
                <h2>para cachorros</h2>
            </div>

            <div class="flex justify-center items-center space-x-10">
                <div class="flex items-center text-white text-[3.2vh] cursor-pointer">
                    <h2>Filtros</h2>
                    <img src="../assets/icones/LimparFiltros.png" alt="">
                </div>

                <div
                    class="bg-white w-[25vh] h-14 flex justify-center items-center rounded-br-[35px] rounded-tl-[35px] border-[2px] border-black pl-4">
                    <select name="ordenar" id="" class=" font-bold text-[2vh]">
                        <option disabled selected>Ordenar Por</option>
                        <option value="volvo">Menor Valor</option>
                        <option value="saab">Maior Valor</option>
                        <option value="opel">Melhor Avaliado</option>
                        <option value="audi">Ordem alfabetica</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-[25%_75%]">

            <div class="flex items-center flex-col">
                <filtro />
            </div>

            <div>
                <div class="grid grid-cols-4 gap-6 text-white">
                    <div v-for="produto in filtrarProduto" :key="produto.id">
                        <Produto :texto="produto.titulo" :valor="produto.valor" :rota="produto.id"
                            :categoria="produto.categoria" :produtoImagem="produto.img_url" />
                    </div>
                </div>
            </div>
        </div>
        <footerPrincipal />
    </div>
</template>

<script>
import headerPrincipal from "@/components/headerPrincipal.vue";
import footerPrincipal from "@/components/footerPrincipal.vue";
import headerCategoria from "@/components/headerCategoria.vue"
import Produto from "@/components/Auxiliar/produtosAux/produto.vue";
import filtro from "@/components/Auxiliar/produtosAux/filtro.vue";

export default {
    components: {
        headerPrincipal,
        footerPrincipal,
        Produto,
        filtro,
        headerCategoria
    },
    data() {
        return {
            produtos: [],
        }
    },
    computed: {
        filtrarProduto() {
            const produtosFiltrados = this.produtos.data?.filter((produto) => produto.categoria === this.$route.params.rota)
            return produtosFiltrados;
        },
    },
    mounted() {
        fetch('http://127.0.0.1:8000/api/produtos')
            .then(api => api.json())
            .then(data => { this.produtos = data,
                console.log(this.filtrarProduto)
            });
    },
};
</script>