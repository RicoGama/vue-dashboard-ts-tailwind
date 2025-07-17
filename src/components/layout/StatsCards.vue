<template>
	<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
		<div v-for="(stat, index) in statsData" 
		:key="index"
		class="stats bg-base-100 shadow dark:bg-white/5 dark:backdrop-blur-md
		dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20"
		>
			<div class="stat">
				<div class="stat-title">{{ stat.title }}</div>
				<div class="stat-value">{{ stat.value }}</div>
				<div class="stat-desc"
				:class="{
					'text-green-500': isPositiveChange(stat.desc),
					'text-red-500': !isPositiveChange(stat.desc),
					}">{{ stat.desc }}</div>
			</div>
		</div>
	</div>
</template>
<script setup lang="ts">
import { ref } from 'vue';

interface statsItem {
	title: string;
	value: string;
	desc: string;
}


const statsData = ref<statsItem[]>([
	{
		title: 'Total Users',
		value: '12.345',
		desc: '↗ 14% from last month',
	},
	{
		title: 'Revenue',
		value: '$42,256',
		desc: '↗ 23% from last month',
	},
	{
		title: 'New Orders',
		value: '56',
		desc: '↘ 5% from last month',
	},
	{
		title: 'Active Projects',
		value: '56',
		desc: '↗ 8% from last month',
	},

]);

const isPositiveChange = (desc: string): boolean => {
	return desc.startsWith('↗');
};
</script>