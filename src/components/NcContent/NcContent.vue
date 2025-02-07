<!--
 - @copyright Copyright (c) 2018 Christoph Wurst <christoph@winzerhof-wurst.at>
 -
 - @author Christoph Wurst <christoph@winzerhof-wurst.at>
 -
 - @license GNU AGPL version 3 or any later version
 -
 - This program is free software: you can redistribute it and/or modify
 - it under the terms of the GNU Affero General Public License as
 - published by the Free Software Foundation, either version 3 of the
 - License, or (at your option) any later version.
 -
 - This program is distributed in the hope that it will be useful,
 - but WITHOUT ANY WARRANTY; without even the implied warranty of
 - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 - GNU Affero General Public License for more details.
 -
 - You should have received a copy of the GNU Affero General Public License
 - along with this program. If not, see <http://www.gnu.org/licenses/>.
 -
 -->

<docs>

### General description

This component provides the default container of all apps.
It _MUST_ be used as the main wrapper of your app.
It includes the Navigation, the App content and the Sidebar.

### Standard usage

```vue
	<template>
		<NcContent app-name="forms">
			<NcAppNavigation>
				<template #list>
					<NcAppNavigationNew text="Create article" />
					<NcAppNavigationItem name="My navigation" title="My title">
						<template #icon>
							<Check :size="20" />
						</template>
					</NcAppNavigationItem>
				</template>
			</NcAppNavigation>
			<NcAppContent>
				<h2>Your main app content here</h2>
				<NcButton @click="opened = !opened">Toggle sidebar</NcButton>
			</NcAppContent>
			<NcAppSidebar v-if="opened" name="cat-picture.jpg" @close="opened=false"></NcAppSidebar>
		</NcContent>
	</template>
	<script>
	import Check from 'vue-material-design-icons/Check'

	export default {
		components: {
			Check,
		},
		data() {
			return {
				opened: false,
			}
		}
	}
	</script>
```

</docs>

<template>
	<div id="content-vue"
		:class="`app-${appName.toLowerCase()}`"
		class="content">
		<slot />
	</div>
</template>

<script>
export default {
	props: {
		appName: {
			type: String,
			required: true,
		},
	},
}
</script>

<style lang="scss" scoped>
.content {
	box-sizing: border-box;
	margin: var(--body-container-margin);
	margin-top: 50px;
	display: flex;
	width: calc(100% - var(--body-container-margin) * 2);
	border-radius: var(--body-container-radius);
	height: var(--body-height);
	overflow: hidden;
	padding: 0;

	&:not(.with-sidebar--full) {
		position: fixed;
	}

	:deep(*) {
		box-sizing: border-box;
	}
}
</style>
