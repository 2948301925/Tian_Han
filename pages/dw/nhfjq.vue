<template>

</template>

<script>
	uni.getLocation({
		type: 'gcj02', //返回可以用于uni.openLocation的经纬度
		success: function (res) {
			const latitude = 32.956186;
			const longitude = 106.897501;
			uni.openLocation({
				latitude: latitude,
				longitude: longitude,
				success: function () {
					console.log('success');
				}
			});
		}
	});
</script>

<style>
	
</style>