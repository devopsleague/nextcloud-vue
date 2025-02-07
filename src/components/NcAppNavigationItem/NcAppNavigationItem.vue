<!--
 - @copyright Copyright (c) 2018 John Molakvoæ <skjnldsv@protonmail.com>
 -
 - @author John Molakvoæ <skjnldsv@protonmail.com>
 - @author Marco Ambrosini <marcoambrosini@icloud.com>
 - @author Jonas Sulzer <jonas@violoncello.ch>
 - @author Jonathan Treffler <mail@jonathan-treffler.de>
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
 - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
 - GNU Affero General Public License for more details.
 -
 - You should have received a copy of the GNU Affero General Public License
 - along with this program. If not, see <http://www.gnu.org/licenses/>.
 -
 -->

<docs>

# Usage

### Simple element

* With an icon:

```vue
	<template>
		<NcAppNavigationItem name="My name">
			<template #icon>
				<Check :size="20" />
			</template>
		</NcAppNavigationItem>
	</template>
	<script>
	import Check from 'vue-material-design-icons/Check'

	export default {
		components: {
			Check,
		},
	}
	</script>
```
* With a spinning loader instead of the icon:

```
<NcAppNavigationItem name="Loading Item" :loading="true" />
```

### Element with actions
Wrap the children in a template. If you have more than 2 actions, a popover menu and a menu
button will be automatically created.

```vue
	<template>
		<div id="app-navigation-vue"><!-- Just a wrapper necessary in the docs. Not needed when NcAppNavigation is correctly used as parent. -->
			<NcAppNavigationItem name="Item with actions">
				<template #icon>
					<Check :size="20" />
				</template>
				<template #actions>
					<NcActionButton @click="alert('Edit')">
						<template #icon>
							<Pencil :size="20" />
						</template>
						Edit
					</NcActionButton>
					<NcActionButton @click="alert('Delete')">
						<template #icon>
							<Delete :size="20" />
						</template>
						Delete
					</NcActionButton>
					<NcActionLink name="Link" href="https://nextcloud.com">
						<template #icon>
							<OpenInNew :size="20" />
						</template>
					</NcActionLink>
				</template>
			</NcAppNavigationItem>
		</div>
	</template>
	<script>
	import Check from 'vue-material-design-icons/Check'
	import Delete from 'vue-material-design-icons/Delete'
	import OpenInNew from 'vue-material-design-icons/OpenInNew'
	import Pencil from 'vue-material-design-icons/Pencil'

	export default {
		components: {
			Check,
			Delete,
			OpenInNew,
			Pencil,
		},
	}
	</script>
```

### Element with counter
Just nest the counter in a template within `<NcAppNavigationItem>` and add `#counter` to it.

```vue
	<template>
		<NcAppNavigationItem name="Item with counter">
			<template #icon>
				<Folder :size="20" />
			</template>
			<template #counter>
				<NcCounterBubble>
					99+
				</NcCounterBubble>
			</template>
		</NcAppNavigationItem>
	</template>
	<script>
	import Folder from 'vue-material-design-icons/Folder'

	export default {
		components: {
			Folder,
		},
	}
	</script>
```

### Element with children

Wrap the children in a template with the `slot` property and use the prop `allowCollapse` to choose wether to allow or
prevent the user from collapsing the items.

```vue
	<template>
		<NcAppNavigationItem name="Item with children" :allowCollapse="true" :open="true">
			<template #icon>
				<Folder :size="20" />
			</template>
			<template #counter>
				<NcCounterBubble>
					99+
				</NcCounterBubble>
			</template>
			<template #actions>
				<NcActionButton @click="alert('Edit')">
					<template #icon>
						<Pencil :size="20" />
					</template>
					Edit
				</NcActionButton>
				<NcActionButton @click="alert('Delete')">
					<template #icon>
						<Delete :size="20" />
					</template>
					Delete
				</NcActionButton>
				<NcActionLink name="Link" href="https://nextcloud.com">
					<template #icon>
						<OpenInNew :size="20" />
					</template>
				</NcActionLink>
			</template>
			<template>
				<NcAppNavigationItem name="AppNavigationItemChild1" />
				<NcAppNavigationItem name="AppNavigationItemChild2" />
				<NcAppNavigationItem name="AppNavigationItemChild3" />
				<NcAppNavigationItem name="AppNavigationItemChild4" />
			</template>
		</NcAppNavigationItem>
	</template>
	<script>
	import Folder from 'vue-material-design-icons/Folder'
	import Delete from 'vue-material-design-icons/Delete'
	import OpenInNew from 'vue-material-design-icons/OpenInNew'
	import Pencil from 'vue-material-design-icons/Pencil'

	export default {
		components: {
			Folder,
			Delete,
			OpenInNew,
			Pencil,
		},
	}
	</script>
```

### Editable element
Add the prop `:editable=true` and an edit placeholder if you need it. By default
the placeholder is the previous name of the element.

```vue
	<template>
		<NcAppNavigationItem name="Editable Item" :editable="true"
			editPlaceholder="your_placeholder_here" @update:name="function(value){alert(value)}">
			<template #icon>
				<Folder :size="20" />
			</template>
		</NcAppNavigationItem>
	</template>
	<script>
	import Folder from 'vue-material-design-icons/Folder'

	export default {
		components: {
			Folder,
		},
	}
	</script>
```

### Undo element
Just set the `undo` and `name` props. When clicking the undo button, an `undo` event is emitted.

```
<NcAppNavigationItem :undo="true" name="Deleted important entry" @undo="alert('undo delete')"  />

```

### Link element
Href that start by http will be treated as external and opened in a new tab
```
<div>
	<NcAppNavigationItem name="Files" href="/index.php/apps/files" />
	<NcAppNavigationItem name="Nextcloud" href="https://nextcloud.com" />
</div>
```

### Custom title
```
<NcAppNavigationItem name="Nextcloud" title="Open the Nextcloud website" href="https://nextcloud.com" />
```

### Pinned element
Just set the `pinned` prop.
```
<NcAppNavigationItem name="Pinned item" :pinned="true" />
```
</docs>

<template>
	<li :id="id"
		:class="{
			'app-navigation-entry--opened': opened,
			'app-navigation-entry--pinned': pinned,
			'app-navigation-entry--collapsible': collapsible,
		}"
		class="app-navigation-entry-wrapper">
		<component :is="isRouterLink ? 'router-link' : 'NcVNodes'"
			v-slot="{ href: routerLinkHref, navigate, isActive }"
			:custom="isRouterLink ? true : false"
			:to="to"
			:exact="isRouterLink ? exact : null">
			<div :class="{
					'app-navigation-entry--editing': editingActive,
					'app-navigation-entry--deleted': undo,
					'active': isActive && to,
				}"
				class="app-navigation-entry">
				<!-- Icon and name -->
				<a v-if="!undo"
					class="app-navigation-entry-link"
					:aria-description="ariaDescription"
					:aria-expanded="opened.toString()"
					:href="href || routerLinkHref || '#'"
					:target="isExternal(href) ? '_blank' : ''"
					:title="title || name"
					@blur="handleBlur"
					@click="onClick($event, navigate, routerLinkHref)"
					@focus="handleFocus"
					@keydown.tab.exact="handleTab">

					<!-- icon if not collapsible -->
					<!-- never show the icon over the collapsible if mobile -->
					<div :class="{ [icon]: icon }"
						class="app-navigation-entry-icon">
						<NcLoadingIcon v-if="loading" />
						<slot v-else name="icon" />
					</div>
					<span v-if="!editingActive" class="app-navigation-entry__name">
						{{ name }}
					</span>
					<div v-if="editingActive" class="editingContainer">
						<NcInputConfirmCancel ref="editingInput"
							v-model="editingValue"
							:placeholder="editPlaceholder !== '' ? editPlaceholder : name"
							@cancel="cancelEditing"
							@confirm="handleEditingDone" />
					</div>
				</a>

				<!-- undo entry -->
				<div v-if="undo" class="app-navigation-entry__deleted">
					<div class="app-navigation-entry__deleted-description">
						{{ name }}
					</div>
				</div>

				<!-- Counter and Actions -->
				<div v-if="hasUtils && !editingActive"
					class="app-navigation-entry__utils"
					:class="{'app-navigation-entry__utils--display-actions': forceDisplayActions || menuOpenLocalValue || menuOpen }">
					<div v-if="$slots.counter"
						class="app-navigation-entry__counter-wrapper">
						<slot name="counter" />
					</div>
					<NcActions v-if="$slots.actions || (editable && !editingActive) || undo"
						ref="actions"
						:inline="inlineActions"
						class="app-navigation-entry__actions"
						container="#app-navigation-vue"
						:boundaries-element="actionsBoundariesElement"
						:placement="menuPlacement"
						:open="menuOpen"
						:force-menu="forceMenu"
						:default-icon="menuIcon"
						@update:open="onMenuToggle">
						<template #icon>
							<!-- @slot Slot for the custom menu icon -->
							<slot name="menu-icon" />
						</template>
						<NcActionButton v-if="editable && !editingActive"
							:aria-label="editButtonAriaLabel"
							@click="handleEdit">
							<template #icon>
								<Pencil :size="20" />
							</template>
							{{ editLabel }}
						</NcActionButton>
						<NcActionButton v-if="undo"
							:aria-label="undoButtonAriaLabel"
							@click="handleUndo">
							<template #icon>
								<Undo :size="20" />
							</template>
						</NcActionButton>
						<slot name="actions" />
					</NcActions>
				</div>
				<NcAppNavigationIconCollapsible v-if="collapsible" :open="opened" @click.prevent.stop="toggleCollapse" />

				<!-- Anything (virtual) that should be mounted in the component, like a related modal -->
				<slot name="extra" />
			</div>
		</component>
		<!-- Children elements -->
		<ul v-if="canHaveChildren && hasChildren" class="app-navigation-entry__children">
			<slot />
		</ul>
	</li>
</template>

<script>
import NcActions from '../NcActions/index.js'
import NcActionButton from '../NcActionButton/index.js'
import NcLoadingIcon from '../NcLoadingIcon/index.js'
import NcVNodes from '../NcVNodes/index.js'
import NcAppNavigationIconCollapsible from './NcAppNavigationIconCollapsible.vue'
import isMobile from '../../mixins/isMobile/index.js'
import NcInputConfirmCancel from './NcInputConfirmCancel.vue'
import { t } from '../../l10n.js'
import GenRandomId from '../../utils/GenRandomId.js'

import Pencil from 'vue-material-design-icons/Pencil.vue'
import Undo from 'vue-material-design-icons/Undo.vue'

export default {
	name: 'NcAppNavigationItem',

	components: {
		NcActions,
		NcActionButton,
		NcAppNavigationIconCollapsible,
		NcInputConfirmCancel,
		NcLoadingIcon,
		NcVNodes,
		Pencil,
		Undo,
	},

	mixins: [isMobile],

	props: {
		/**
		 * The main text content of the entry.
		 */
		name: {
			type: String,
			required: true,
		},

		/**
		 * The title attribute of the element.
		 */
		title: {
			type: String,
			default: null,
		},

		/**
		 * id attribute of the list item element
		 */
		id: {
			type: String,
			default: () => 'app-navigation-item-' + GenRandomId(),
			validator: id => id.trim() !== '',
		},

		/**
		 * Refers to the icon on the left, this prop accepts a class
		 * like 'icon-category-enabled'.
		 */
		icon: {
			type: String,
			default: '',
		},

		/**
		 * Displays a loading animated icon on the left of the element
		 * instead of the icon.
		 */
		loading: {
			type: Boolean,
			default: false,
		},

		/**
		 * Passing in a route will make the root element of this
		 * component a `<router-link />` that points to that route.
		 * By leaving this blank, the root element will be a `<li>`.
		 */
		to: {
			type: [String, Object],
			default: null,
		},

		/**
		 * A direct link. This will be used as the `href` attribute.
		 * This will ignore any `to` prop being defined.
		 */
		href: {
			type: String,
			default: null,
		},

		/**
		 * Pass in `true` if you want the matching behaviour to
		 * be non-inclusive: https://router.vuejs.org/api/#exact
		 */
		exact: {
			type: Boolean,
			default: false,
		},
		/**
		 * Gives the possibility to collapse the children elements into the
		 * parent element (true) or expands the children elements (false).
		 */
		allowCollapse: {
			type: Boolean,
			default: false,
		},

		/**
		 * Makes the name of the item editable by providing an `ActionButton`
		 * component that toggles a form
		 */
		editable: {
			type: Boolean,
			default: false,
		},

		/**
		 * Only for 'editable' items, sets label for the edit action button.
		 */
		editLabel: {
			type: String,
			default: '',
		},

		/**
		 * Only for items in 'editable' mode, sets the placeholder text for the editing form.
		 */
		editPlaceholder: {
			type: String,
			default: '',
		},

		/**
		 * Pins the item to the bottom left area, above the settings. Do not
		 * place 'non-pinned' `AppnavigationItem` components below `pinned`
		 * ones.
		 */
		pinned: {
			type: Boolean,
			default: false,
		},

		/**
		 * Puts the item in the 'undo' state.
		 */
		undo: {
			type: Boolean,
			default: false,
		},

		/**
		 * The navigation collapsible state (synced)
		 */
		open: {
			type: Boolean,
			default: false,
		},

		/**
		 * The actions menu open state (synced)
		 */
		menuOpen: {
			type: Boolean,
			default: false,
		},

		/**
		 * Force the actions to display in a three dot menu
		 */
		forceMenu: {
			type: Boolean,
			default: false,
		},

		/**
		 * The action's menu default icon
		 */
		menuIcon: {
			type: String,
			default: undefined,
		},

		/**
		 * The action's menu direction
		 */
		menuPlacement: {
			type: String,
			default: 'bottom',
		},

		/**
		 * Entry aria details
		 */
		ariaDescription: {
			type: String,
			default: null,
		},

		/**
		 * To be used only when the elements in the actions menu are very important
		 */
		forceDisplayActions: {
			type: Boolean,
			default: false,
		},

		/**
		 * Number of action items outside the menu
		 */
		inlineActions: {
			type: Number,
			default: 0,
		},
	},

	emits: [
		'update:menuOpen',
		'update:open',
		'update:name',
		'click',
		'undo',
	],

	data() {
		return {
			editingValue: '',
			opened: this.open, // Collapsible state
			editingActive: false,
			hasChildren: false,
			/**
			 * Tracks the open state of the actions menu
			 */
			menuOpenLocalValue: false,
			focused: false,
		}
	},

	computed: {
		isRouterLink() {
			return this.to && !this.href
		},

		collapsible() {
			return this.allowCollapse && !!this.$slots.default
		},

		// Checks if the component is already a children of another
		// instance of AppNavigationItem
		canHaveChildren() {
			if (this.$parent.$options._componentTag === 'AppNavigationItem') {
				return false
			} else {
				return true
			}
		},

		hasUtils() {
			if (this.$slots.actions || this.$slots.counter || this.editable || this.undo) {
				return true
			}
			return false
		},

		editButtonAriaLabel() {
			return this.editLabel ? this.editLabel : t('Edit item')
		},

		undoButtonAriaLabel() {
			return t('Undo changes')
		},
		actionsBoundariesElement() {
			return document.querySelector('#content-vue') || undefined
		},
	},

	watch: {
		open(newVal) {
			this.opened = newVal
		},
	},

	created() {
		this.updateSlotInfo()
	},

	beforeUpdate() {
		this.updateSlotInfo()
	},

	methods: {
		// sync opened menu state with prop
		onMenuToggle(state) {
			this.$emit('update:menuOpen', state)
			this.menuOpenLocalValue = state
		},
		// toggle the collapsible state
		toggleCollapse() {
			this.opened = !this.opened
			this.$emit('update:open', this.opened)
		},

		/**
		 * Handle link click
		 *
		 * @param {PointerEvent} event - Native click event
		 * @param {Function} [navigate] - VueRouter link's navigate if any
		 * @param {string} [routerLinkHref] - VueRouter link's href
		 */
		onClick(event, navigate, routerLinkHref) {
			// Always forward native event
			this.$emit('click', event)
			// Do not navigate with control keys - it is opening in a new tab
			if (event.metaKey || event.altKey || event.ctrlKey || event.shiftKey) {
				return
			}
			// Prevent default link behaviour if it's a router-link and navigate manually
			if (routerLinkHref) {
				navigate?.(event)
				event.preventDefault()
			}
		},

		// Edition methods
		handleEdit() {
			this.editingValue = this.name
			this.editingActive = true
			this.onMenuToggle(false)
			this.$nextTick(() => {
				this.$refs.editingInput.focusInput()
			})
		},
		cancelEditing() {
			this.editingActive = false
		},
		handleEditingDone() {
			this.$emit('update:name', this.editingValue)
			this.editingValue = ''
			this.editingActive = false
		},

		// Undo methods
		handleUndo() {
			this.$emit('undo')
		},

		updateSlotInfo() {
			this.hasChildren = !!this.$slots.default
		},

		/**
		 * Show actions upon focus
		 */
		handleFocus() {
			this.focused = true
		},

		handleBlur() {
			this.focused = false
		},

		/**
		 * This method checks if the root element of the component is focused and
		 * if that's the case it focuses the actions button if available
		 *
		 * @param {Event} e the keydown event
		 */
		handleTab(e) {
			// If there is no actions menu, do nothing.
			if (!this.$refs.actions) {
				return
			}
			if (this.focused) {
				e.preventDefault()
				this.$refs.actions.$refs.menuButton.$el.focus()
				this.focused = false
			} else {
				this.$refs.actions.$refs.menuButton.$el.blur()
			}
		},

		/**
		 * Is this an external link
		 *
		 * @param {string} href The link to check
		 * @return {boolean} Whether it is external or not
		 */
		isExternal(href) {
			// Match any protocol
			return href && href.match(/[a-z]+:\/\//i)
		},
	},
}
</script>

<style lang="scss">
.app-navigation-entry {
	position: relative;
	display: flex;
	flex-shrink: 0;
	flex-wrap: wrap;
	box-sizing: border-box;
	width: 100%;
	min-height: $clickable-area;
	transition: background-color var(--animation-quick) ease-in-out;
	transition: background-color 200ms ease-in-out;
	border-radius: var(--border-radius-pill);

	&-wrapper {
		position: relative;
		display: flex;
		flex-shrink: 0;
		flex-wrap: wrap;
		box-sizing: border-box;
		width: 100%;

		&.app-navigation-entry--collapsible:not(.app-navigation-entry--opened) > ul {
			// NO ANIMATE because if not really hidden, we can still tab through it
			display: none;
		}
	}

	// When .active class is applied, change color background of link and utils. The
	// !important prevents the focus state to override the active state.
	&.active {
		background-color: var(--color-primary-element) !important;

		// overwrite active text color
		.app-navigation-entry-link, .app-navigation-entry-button {
			color: var(--color-primary-element-text) !important;
		}
	}
	&:focus-within,
	&:hover {
		background-color: var(--color-background-hover);
	}
	&.active,
	&:focus-within,
	&:hover {
		.app-navigation-entry__children {
			background-color: var(--color-main-background);
		}
	}

	// Show the actions on active
	&.active,
	// Always show the undo button
	&.app-navigation-entry--deleted,
	&:focus,
	&:focus-within,
	&:hover {
		.app-navigation-entry__utils .app-navigation-entry__actions {
			display: inline-block;
		}
	}

	/* hide deletion/collapse of subitems */
	&.app-navigation-entry--deleted > ul {
		// NO ANIMATE because if not really hidden, we can still tab through it
		display: none;
	}

	&:not(.app-navigation-entry--editing) {
		.app-navigation-entry-link, .app-navigation-entry-button {
			padding-right: $icon-margin;
		}
	}

	// Main entry link
	.app-navigation-entry-link, .app-navigation-entry-button {
		z-index: 100; /* above the bullet to allow click*/
		display: flex;
		overflow: hidden;
		flex: 1 1 0;
		box-sizing: border-box;
		min-height: $clickable-area;
		padding: 0;
		white-space: nowrap;
		color: var(--color-main-text);
		background-repeat: no-repeat;
		background-position: $icon-margin center;
		background-size: $icon-size $icon-size;
		line-height: $clickable-area;

		.app-navigation-entry-icon {
			display: flex;
			align-items: center;
			flex: 0 0 $clickable-area;
			justify-content: center;
			width: $clickable-area;
			height: $clickable-area;
			background-size: $icon-size $icon-size;
			background-repeat: no-repeat;
			background-position: $icon-margin center;
		}

		.app-navigation-entry__name {
			overflow: hidden;
			max-width: 100%;
			white-space: nowrap;
			text-overflow: ellipsis;
		}

		.editingContainer {
			width: calc(100% - #{$clickable-area});
			margin: auto;
		}
	}
}
/* Second level nesting for lists */
.app-navigation-entry__children {
	position: relative;
	display: flex;
	flex: 0 1 auto;
	flex-direction: column;
	width: 100%;
	gap: var(--default-grid-baseline, 4px);

	.app-navigation-entry {
		display: inline-flex;
		flex-wrap: wrap;
		padding-left: $icon-size;
	}
}

/* Deleted entries */
.app-navigation-entry__deleted {
	display: inline-flex;
	flex: 1 1 0;
	padding-left: $clickable-area - $icon-margin !important;
	.app-navigation-entry__deleted-description {
		position: relative;
		overflow: hidden;
		flex: 1 1 0;
		white-space: nowrap;
		text-overflow: ellipsis;
		line-height: $clickable-area;
	}
}

/* counter and actions */
.app-navigation-entry__utils {
	display: flex;
	min-width: $clickable-area;
	align-items: center;
	flex: 0 1 auto;
	justify-content: flex-end;
	&#{&}--display-actions .action-item.app-navigation-entry__actions {
		display: inline-block;
	}
	/* counter */
	.app-navigation-entry__counter-wrapper {
		// Add slightly more space to the right of the counter
		margin-right: calc(var(--default-grid-baseline) * 3);
		display: flex;
		align-items: center;
		flex: 0 1 auto;
	}
	/* actions */
	.action-item.app-navigation-entry__actions {
		display: none;
	}
}

// STATES
/* editing state */
.app-navigation-entry--editing {
	.app-navigation-entry-edit {
		z-index: 250;
		opacity: 1;
	}
}

/* deleted state */
.app-navigation-entry--deleted {
	.app-navigation-entry-deleted {
		z-index: 250;
		transform: translateX(0);
	}
}

/* pinned state */
.app-navigation-entry--pinned {
	order: 2;
	margin-top: auto;
	// only put a marginTop auto to the first one!
	~ .app-navigation-entry--pinned {
		margin-top: 0;
	}
}

// Add more contrast for active entry
[data-themes*='highcontrast'] {
	.app-navigation-entry {
		&:active {
			background-color: var(--color-primary-element-light-hover) !important;
		}
	}
}
</style>
