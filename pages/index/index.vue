<template>
	<view class="content">
		<map style="width: 100%; height: 100%;" 
			:latitude = "latitude" 
			:longitude = "longitude" 
			:markers = "covers"
			:scale = "scale"
			:show-location = "true"
			@markertap = "markerClick"
			@tap = "mapTapClick">
			<cover-view class="map-search-box">
				<cover-view class="search-content">
					<cover-image class="search-icon" src="../../static/search.png"></cover-image>
					<cover-view class="search-input">请输入搜索内容</cover-view>
				</cover-view>
			</cover-view>
			<cover-view class=".map-controls-location">
				<cover-image 
					@click="locationClick" src="../../static/location.png">
				</cover-image>
			</cover-view>
			<cover-view v-show="isDetails" class="popup map-marker-details">
				<cover-view class="marker-details-content">
					<cover-view class="marker-details-title">{{foodShop[id]['name']}}</cover-view>
					<cover-view class="marker-details-add">{{foodShop[id]['add']}}</cover-view>
				</cover-view>
			</cover-view>
		</map>
	</view>
</template>
 
<script>	
	export default {
		data() {
			return {
				title: 'map',
				latitude: 22.194658,
				longitude: 113.550676,
				scale: 15,
				covers: [{
					id: '0',
					latitude: 22.18905,
					longitude: 113.546877,
					iconPath: '../../static/eatery_point.png'
				}, {
					id: '1',
					latitude: 22.195074,
					longitude: 113.553416,
					iconPath: '../../static/eatery_point.png'
				},
				{
					id: '2',
					latitude: 22.198855,
					longitude: 113.554027,
					iconPath: '../../static/eatery_point.png'
				},
				{
					id: '3',
					latitude: 22.204309,
					longitude: 113.548781,
					iconPath: '../../static/eatery_point.png'
				},
				{
					id: '4',
					latitude: 22.204945,
					longitude: 113.557477,
					iconPath: '../../static/eatery_point.png'
				},
				{
					id: '5',
					latitude: 22.211246,
					longitude: 113.554773,
					iconPath: '../../static/eatery_point.png'
				}],
				isDetails: false,
				id: '',
				foodShop: [
					{
						name: '亚利咖喱屋',
						add: '澳門特別行政區風順堂區半島西灣民國大馬路4號K地下'
					},
					{
						name: '玛嘉烈蛋挞',
						add: '澳門特別行政區大堂區賈伯樂提督街41號A'
					},
					{
						name: '蕃茄屋葡式美食',
						add: '澳門特別行政區大堂區連安后巷富安大廈4號及6號地下'
					},
					{
						name: '六記粥麵',
						add: '澳門特別行政區花王堂區仁慕巷1-D'
					},
					{
						name: '馬慶康南天咖啡室',
						add: '澳門特別行政區花王堂區半島俾利喇街63號A65號B'
					},
					{
						name: '新苗超市(永安街)',
						add: '澳門特別行政區花地瑪堂區永定街94-100號南晖商場'
					}
				]
			}
		},
		onLoad() {
			// this.getLocation();
		},
		methods: {
			getLocation() {
				uni.getLocation({
					type: 'wgs84',
					success: (function (res) {
						this.latitude = res.latitude;
						this.longitude = res.longitude;
					}).bind(this)
				})
			},
			
			locationClick() {
				this.getLocation();
			},
			
			markerClick(marker) {
				this.isDetails = true;
				this.id = marker.markerId;
			},
			
			mapTapClick() {
				if (this.isDetails) {
					this.isDetails = false;
				}
			}
		
		}
	}
</script>

<style>
	.content {
		width: 100%;
		height: 100%;
	}
	
	.map-search-box {
		position: absolute;
		top: 1%;
		left: 28upx;
		right: 28upx;
	}
	
	.map-controls-location {
		position: absolute;
		bottom: 18%;
		right: 28upx;
		width: 120upx;
		height: 120upx;
	}
	
	.map-marker-details {
		left: 0;
		bottom: 0;
		width: 100%;
	}
	
	.marker-details-content {
		width: 100%;
		text-align:start;
		margin:15px 0px;
	}
	
	.marker-details-title {
		display: block;
		line-height: 21px;
		margin-left: 18px;
		margin-bottom: 8px;
		font-size: 16px;
		color: #111;
		font-weight: 700;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	
	.marker-details-add {
		display: block;
		line-height: 18px;
		margin-top: 15px;
		margin-left: 18px;
		font-size: 13px;
		padding: 0;
		position: relative;
		vertical-align: bottom;
		color: #666;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	
	.mask {
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
	}
	
	.popup {
		position: fixed;
		background-color: #ffffff;
	}
	
	.search-content {
		width:100%;
		display:flex;
		align-items: center;
		border-radius:60px;
		border:1px #f5f5f5 solid;
		color: #FFFFFF;
		background:rgba(0,0,0, 0.5);
	}
	
	.search-icon {
		padding:0 15upx 0 20upx;
		width: 40upx;
		height: 40upx;
		font-family:iconfont;
		font-size:32rpx;
		font-style:normal;
	}
	
	.search-input {
		display:block;
		width:100%;
		max-width:100%;
		line-height:65rpx;
		height:65rpx;
		cursor:auto;
		text-overflow:clip;
		overflow:hidden;
		white-space:nowrap;
		font-family:UICTFontTextStyleBody;
		min-height:1.4rem;
	}
	
</style>
