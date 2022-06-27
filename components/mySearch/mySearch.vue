<template>
	<view>
		<view class="my-search-container" :style="{ 'background-color': bgcolor }" @click="searchBoxHandler">
		  <view class="my-search-box" :style="{ 'border-radius': radius + 'px' }">
		    <!-- 使用 uni-ui 提供的图标组件 -->
		    <uni-icons type="search" size="17"></uni-icons>
		    <text class="placeholder">搜索</text>
		  </view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"mySearch",
		props: {
		  // 背景颜色
		  bgcolor: {
		    type: String,
		    default: '#d60000'
		  },
		  // 圆角尺寸
		  radius: {
		    type: Number,
		    default: 18 ,// px
				}
		},
		data() {
			return {
				
			};
		},
		methods: {
		  searchBoxHandler() {
				// console.log("搜索框被点击了");
		    this.$emit('click')
		  }
		}
	}
</script>

<style lang="scss">
.my-search-container {
    height: 50px;
    display: flex;
    align-items: center;
    padding: 0 10px;

    .my-search-box {
      height: 36px;
      background-color: #FFFFFF;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;

      .placeholder {
        font-size: 15px;
        margin-left: 5px;
      }
    }
  }
</style>