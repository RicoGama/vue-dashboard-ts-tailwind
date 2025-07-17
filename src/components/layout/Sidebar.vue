<template>
	<aside class="drawer-side bg-white dark:bg-backgroundDark border-r border-gray-200 dark:border-primary/10">
		<label for="my-drawer" aria-label="Fechar Sidebar" class="drawer-overlay"></label>
		<nav class="menu p-4 w-80 min-h-full text-gray-800 dark:text-gray-200" aria-label="Menu">
			<header class="mb-4 flex p-4">
				<h1 class="text-xl font-bold dark:text-white">AdminPanel</h1>
			</header>
			<ul role="menu">
				<li role="none" class="p-2" v-for="(link, index) in links" :key="index">
					<button role="menuitem" :aria-expanded="!!link.children && link.open" :aria-haspopup="!!link.children"
						:class="{ 'active': link.active }" @click="setActive(index)" class="flex items-center w-full text-left hover:bg-gray-100 dark:hover:bg-white/10
					text-black dark:text-white">
						<Icon :icon="link.icon" class="w-5 h-5" />
						<span class="ml-2">{{ link.name }}</span>
						<span v-if="link.children" class="ml-auto dropdown-icon">
							<Icon :icon="link.open ? 'line-md:chevron-down' : 'line-md:chevron-right'" class="w-5 h-5" />
						</span>
					</button>
					<ul v-if="link.children && link.open" class="ml-4 pl-4 border-gray-200 dark:border-white/10">
						<li v-for="(child, childIndex) in link.children" :key="childIndex">
							<a href="#" class="block py-1 hover:bg-gray-100 dark:hover:bg-white/10 text-black dark:text-white">
								{{ child.name }}
							</a>
						</li>
					</ul>
				</li>
			</ul>
		</nav>
	</aside>
</template>
<script setup lang="ts">
import { Icon } from '@iconify/vue';
import { ref } from 'vue';

interface LinkItem {
	name: string
	icon: string
	active: boolean
	open: boolean
	children?: {
		name: string
	}[]
}

const links = ref<LinkItem[]>([
	{
		name: 'Dashboard',
		icon: 'line-md:home',
		active: true,
		open: false,
	},
	{
		name: 'Analytics',
		icon: 'icon-park-outline:chart-line',
		active: false,
		open: false,
	},
	{
		name: 'Reports',
		icon: 'line-md:document-list',
		active: true,
		open: false,
	},
	{
		name: 'Users',
		icon: 'line-md:account',
		active: false,
		open: true,
		children: [
			{
				name: 'All Users',
			},
			{
				name: 'Add New',
			},
			{
				name: 'Roles & Permissions',
			},
		]
	},
	{
		name: 'Products',
		icon: 'mdi:shopping-outline',
		active: false,
		open: false,
		children: [
			{
				name: 'All Products',
			},
			{
				name: 'Categories',
			},
			{
				name: 'Inventory',
			},
		]
	},
	{
		name: 'Messages',
		icon: 'line-md:email',
		active: false,
		open: false,
	},
	{
		name: 'Settings',
		icon: 'line-md:cog-filled',
		active: false,
		open: false,
	},
]);

const setActive = (index: number): void => {
	if (links.value[index].children) {
		links.value[index].open = !links.value[index].open;
	}

	links.value.forEach((link, i) => {
		link.active = i === index;
	});
};
</script>