<template>
	<div class="cartcontrol">
		<transition name="move" enter-active-class="animated slideInRight" leave-active-class="animated slideOutRight">
			<div class="cart-decrease icon-shopping_cart2" v-show="food.count>0" @click="decreaseCart"></div>
		</transition>
		<transition  name="move" enter-active-class="animated slideInRight" leave-active-class="animated slideOutRight">
			<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
		</transition>
		<div class="cart-add icon-add_circle" @click="addCart"></div>
	</div>
</template>
<script>
	import Vue from 'vue';
	export default{
		props:{
			food:{
				type:Object
			}
		},
		methods:{
			addCart(event){
				if(!event._constructed){
					return;
				}
				if(!this.food.count){
					Vue.set(this.food,'count',1);
				}else{
					this.food.count++;
				}
			},
			decreaseCart(event){
				if(!event._constructed){
					return;
				}
				if(this.food.count>0){
					this.food.count--;
				}
			}
		}
	}
</script>
<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size:0
		.cart-decrease,.cart-add
			display:inline-block
			padding:6px
			font-size:24px
			line-hight:24px
			color:rgb(0,160,220)
		.cart-count
			display:inline-block
			vertical-align:top
			width:12px
			padding-top:6px
			line-height:24px
			text-align:center
			font-size:10px
			color:rgb(147,153,159)
			
</style>