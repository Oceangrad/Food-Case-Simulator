<template>
    <div :style="'width: 120%; background-color: ' + currentProduct.rarity.color">
        <p>
            name: {{ currentProduct.name }}
            <br>
            rarity: {{ currentProduct.rarity.name }}
        </p>
        <img :src="currentProduct.img">
    </div>
    <br>
    <button @click="this.currentProduct = GetRandomProductByProbability()">Open new Food Case</button>
</template>

<script>
import Product from '../model/Product';
import rarities from '../model/Rarities';

export default{
    name: "Probability",
    data() {
        return{
            products: [
                new Product("banana", "src/assets/img/banana.jpg", 1, rarities.legend),
                new Product("apple", "src/assets/img/apple.jpg", 5, rarities.epic),
                new Product("orange", "src/assets/img/orange.jpg", 10, rarities.rare),
                new Product("pelmeni", "src/assets/img/pelmeni.jpg", 19, rarities.rare),
                new Product("chipseki", "src/assets/img/chips.jpg", 25, rarities.common),
                new Product("okorochek", "src/assets/img/okorochek.jpg", 40, rarities.common),
            ],
            currentProduct: 0,
        }
    },
    created(){
        this.currentProduct = this.GetRandomProductByProbability();
    },
    methods: {
        GetRandomProductByProbability(){
            var product = this.products[this.products.length-1];
            var chance = Math.random() * 100;
            for(var i = 0; i < this.products.length-1; i++){
                if(chance <= this.products[i].probability){
                    product = this.products[i];
                    break;
                }
            }
            return product;
        }
    }
}
</script>

<style scoped>
    img{
        height: 250px;
    }
    p{
        background-color: antiquewhite;
    }
</style>>