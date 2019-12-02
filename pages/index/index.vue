<template>
	<view class="content">
		<view class="calendar">
			<view class="dayFrame" v-for="count in 35">
				<view class="day" v-if="noEmpty(count)" @click="c(count-firstDay+1)">
					<view class="dayNum">{{count-firstDay+1}}</view>
					<solt :day="count-firstDay+1"></solt>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import moment from 'moment'
	export default {
		data() {
			return {
				year:2019,
				month:12,
				date:2
			}
		},
		onLoad() {

		},
		methods: {
			firstDay(){
				return moment(this.year+'-'+this.month+"-"+this.date,'YYYY-MM-DD').format('e')
			},
			lastDay(){
				return moment(this.year+'-'+this.month+"-"+this.date,'YYYY-MM-DD').endOf('month').format('DD')
			},
			noEmpty(num){
				if(num - this.lastDay()>this.firstDay()){
					return false;
				}else{
					return true;
				}
			},
			c(day){
				this.$emit("clickDay",day)
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
