<template>
    <view>
        <view class="page-body">
            <view class="page-section page-section-gap">
                <map style="width: 100%; height:calc(100vh - 250upx);" :latitude="latitude" :longitude="longitude" :markers="covers">
                </map>
            </view>
        </view>
    </view>
</template>

<script>
	export default {
	    data() {
	        return {
	      id:0, // 使用 marker点击事件 需要填写id
	            title: 'map',
	            latitude: 42.16149799999999,
	            longitude: 114.56000799999993,
	            covers: [{
	                latitude: 42.16149799999999,
	                longitude: 114.56000799999993,
	                // iconPath: '../../../static/location.png'
	            }, {
	                latitude: 42.16149799999999,
	                longitude: 114.56000799999993,
	                // iconPath: '../../../static/location.png'
	            }]
	        }
	    },
	    methods: {
	
	    }
	}
</script>

<style>
</style>
