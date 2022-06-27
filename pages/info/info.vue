<template>
	<view class="container">
		<!-- 用户未登录时，显示登录组件 -->
		<myLogin v-if="!token"></myLogin>

		<!-- 用户登录后，显示用户信息组件 -->
		<myUserinfo v-else></myUserinfo>
	</view>
</template>

<script>
	import badgeMix from '@/mixins/tabbar-badge.js'
	import {
		mapState
	} from 'vuex'
	export default {
		mixins: [badgeMix],
		data() {
			return {

			}

		},
		methods: {
		
		},
		computed: {
			...mapState('m_user', ['token']),
		}
	}
</script>

<style lang="scss" scoped>

</style>
