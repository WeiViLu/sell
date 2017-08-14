<template>
	<div class="goods">
		<div class="menu-wrapper">
			<ul>
				<li v-for="item in goods" class="menu-item">
					<span class="text border-1px">
						<span class="icon" v-show="item.type>0" :class="classMap[item.type]"></span>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper">
			<ul>
				<li v-for="item in goods" class="food-list">
					<h1 class="tittle">{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item">
							<div class="icon">
								<img :src="food.icon" alt="">
							</div>
							<div class="content">
								<h2 class="name">{{food.name}}</h2>
								<p class="desc">{{food.description}}</p>
								<div class="extra">
									<span>月售{{food.sellCount}}份</span>
									<span>好评率{{food.rating}}%</span>
								</div>
							</div>
							<div class="price">
								<span>¥{{food.price}}</span>
								<span v-show="food.oldPrice">¥{{food.oldPrice}} </span>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>
<script>
const ERR_OK=0;
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return{
				goods:[]
			}
		},
		created(){
			this.classMap=['decrease','discount','special','invoice','guarantee'];
			this.$http.get('api/goods').then((response)=>{
				response=response.body;
				if(response.errno===ERR_OK){
					this.goods=response.data;
				}
			})
		}
	}
</script>
<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin"
	.goods
		display:flex
		position:absolute
		top:174px
		bottom:46px
		width:100%
		overflow:hidden
		.menu-wrapper
			flex:0 0 80px
			width:80px
			text-align:center
			background:#f3f5f7
			.menu-item
				display:table 
				height:54px
				width:56px
				line-height:14px
				padding:0 12px
				.icon
					display:inline-block
					vertical-align:top
					width:12px
					height:12px
					margin-right:2px
					background-size:12px 12px
					background-repeat:no-repeat
					&.decrease
						bg-image('../../resource/img/decrease_3')	
					&.discount
						bg-image('../../resource/img/discount_3')
					&.guarantee	
						bg-image('../../resource/img/guarantee_3')	
					&.invoice
						bg-image('../../resource/img/invoice_3')
					&.special
						bg-image('../../resource/img/special_3')					
				.text
					display:table-cell
					width:56px
					vertical-align:middle
					border-1px(rgba(7,17,27,0.1))
					font-size:12px	
		.foods-wrapper
			flex:1
			
		
</style>