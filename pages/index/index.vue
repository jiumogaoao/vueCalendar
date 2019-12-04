<template>
	<view class="content">
		<calendarCP :year="year" :month="month" :date="date" :selected="selected" @clickDay="chooseDay">
			<template v-slot:default="message">
				<!-- 获取日期 <view>{{message.day}}</view> -->
				<!-- 是否已选<view>{{message.isSelected}}</view> -->
				<!-- 是否周日<view>{{message.isSunday}}</view> -->
				<!-- 是否周六<view>{{message.isSaturday}}</view> -->
				<!-- 是否当天<view>{{message.isToday}}</view> -->
				<view>{{message.isSelected?'选了':''}}</view>
			</template>
		</calendarCP>
	</view>
</template>

<script>
	
	import calendarCP from "@/component/calendar_CP.vue"
	export default {
		components:{
			calendarCP
		},
		data() {
			return {
				'year':2019,
				'month':12,
				'date':4,
				'selected':[1,3,5,7,9]
			}
		},
		onLoad() {

		},
		methods: {
			chooseDay(data){
				console.log(data)
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
</style>
