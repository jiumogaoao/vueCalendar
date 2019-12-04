<template>
	<view class="calendarCP">
		<view :class="{dayFrame:1,isSelected:isSelected(count-firstDay),isSunday:isSunday(count-1),isSaturday:isSaturday(count-1),isToday:isToday(count-firstDay)}" v-for="count in 35" :key="count" :count="count">
			<view class="day" v-if="noEmpty(count-1)&&((count-firstDay)>0)" 
			@click="c({
				day:count-firstDay,
				isToday:isToday(count-firstDay),
				isSelected:isSelected(count-firstDay),
				isSunday:isSunday(count-1),
				isSaturday:isSaturday(count-1)
				})">
				<view class="dayNum">{{isToday(count-firstDay)?'今天':(count-firstDay)}}</view>
				<slot 
				:day="count-firstDay" 
				:isToday="isToday(count-firstDay)" 
				:isSelected="isSelected(count-firstDay)" 
				:isSunday="isSunday(count-1)" 
				:isSaturday="isSaturday(count-1)"></slot>
			</view>
		</view>
	</view>
</template>

<script>
	import moment from 'moment'
	export default {
		props: ['year','month','date','selected'],
		data() {
			return {

			}
		},
		methods:{
			isToday(num){
				let today = moment().format('YYYY-MM-DD')
				let chooseDay = this.year+'-'+(this.month<10?('0'+this.month):this.month)+"-"+(num<10?('0'+num):num)
				if(chooseDay==today){
					return true
				}else{
					return false
				}
			},
			isSaturday(num){
				if(num%7==6){
					return true
				}else{
					return false
				}
			},
			isSunday(num){
				if(num%7){
					return false
				}else{
					return true
				}
			},
			isSelected(num){
				if(!this.selected.length){return false}
				let select = false;
				this.selected.map(function(v){
					if(v==num){
						select = true;
					}
				})
				return select;
			},
			noEmpty(num){
				if(num - this.lastDay>=this.firstDay){
					return false;
				}else{
					return true;
				}
			},
			c(dayMessage){
				this.$emit("clickDay",dayMessage)
			}
		},
		computed: {
			firstDay(){
				console.log("firstDay",moment(this.year+'-'+(this.month<10?('0'+this.month):this.month)+"-01",'YYYY-MM-DD').format('e'))
				return Number(moment(this.year+'-'+(this.month<10?('0'+this.month):this.month)+"-01",'YYYY-MM-DD').format('e'))
			},
			lastDay(){
				console.log("lastDay",moment(this.year+'-'+(this.month<10?('0'+this.month):this.month)+"-"+(this.date<10?('0'+this.date):this.date),'YYYY-MM-DD').endOf('month').format('DD'))
				return Number(moment(this.year+'-'+(this.month<10?('0'+this.month):this.month)+"-"+(this.date<10?('0'+this.date):this.date),'YYYY-MM-DD').endOf('month').format('DD'))
			}
		}
	}
</script>

<style  lang="scss">
	.calendarCP{
		width:100%;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.dayFrame{
			width: 14.2%;
			height: 200rpx;
			flex-flow: 1;
			background-color: #fff;
			.day{
				width: 100%;
				height: 100%;
				display: flex;
				flex-direction: column;
				align-items: center;
				.dayNum{
					padding-top: 20rpx;
				}
			}
		}
		.dayFrame.isSunday{
			background-color: #d7f3d0;
		},
		.dayFrame.isSaturday{
			background-color: #c4dad2;
		},
		.dayFrame.isToday{
			background-color: #fff7c6;
		},
		.dayFrame.isSelected{
			background-color: #ffbeb5;
		}
	}
</style>
