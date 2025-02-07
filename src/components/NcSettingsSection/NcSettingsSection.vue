<!--
  - @copyright Copyright (c) 2019 Julius Härtl <jus@bitgrid.net>
  -
  - @author Julius Härtl <jus@bitgrid.net>
  - @author Greta Doci <gretadoci@gmail.com>
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
### General description

This component is to be used in the settings section of nextcloud.

### Examples

```vue
<template>
	<NcSettingsSection
		name="Two-Factor Authentication"
		description="Two-factor authentication can be enforced for all users and specific groups."
		doc-url="https://docs.nextcloud.com/server/19/go.php?to=admin-2fa"
		:limit-width="true">
		<p>Your settings here</p>
	</NcSettingsSection>
</template>
```
</docs>

<template>
	<div class="settings-section" :class="{'settings-section--limit-width': limitWidth}">
		<h2 class="settings-section__name">
			{{ name }}
			<a v-if="hasDocUrl"
				:href="docUrl"
				class="settings-section__info"
				role="note"
				:aria-label="docNameTranslated"
				:title="docNameTranslated"
				target="_blank"
				rel="noreferrer nofollow">
				<HelpCircle :size="20" />
			</a>
		</h2>
		<p v-if="hasDescription"
			class="settings-section__desc">
			{{ description }}
		</p>
		<slot />
	</div>
</template>

<script>
import { t } from '../../l10n.js'

import HelpCircle from 'vue-material-design-icons/HelpCircle.vue'

export default {
	name: 'NcSettingsSection',

	components: {
		HelpCircle,
	},

	props: {
		name: {
			type: String,
			required: true,
		},
		description: {
			type: String,
			default: '',
		},
		docUrl: {
			type: String,
			default: '',
		},
		/**
		 * Limit the width of the setting's content
		 *
		 * By default only the name and description have a limit, use this
		 * property to also apply this to the rest of the content.
		 */
		limitWidth: {
			type: Boolean,
			default: true,
		},
	},

	data() {
		return {
			docNameTranslated: t('External documentation for {name}', {
				name: this.name,
			}),
		}
	},

	computed: {
		hasDescription() {
			return this.description.length > 0
		},
		hasDocUrl() {
			return this.docUrl.length > 0
		},
	},
}

</script>

<style lang="scss" scoped>
$maxWidth: 900px;

.settings-section {
	display: block;
	margin-bottom: auto;
	padding: 30px;

	&:not(:last-child) {
		border-bottom: 1px solid var(--color-border);
	}

	&--limit-width > * {
		max-width: $maxWidth;
	}

	&__name {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		font-size: 20px;
		font-weight: bold;
		max-width: $maxWidth;
	}

	&__info {
		display: flex;
		align-items: center;
		justify-content: center;
		width: $clickable-area;
		height: $clickable-area;
		// make sure to properly align the icon with the text
		margin: -$icon-margin;
		margin-left: 0;
		opacity: $opacity_normal;

		&:hover, &:focus, &:active {
			opacity: $opacity_full;
		}
	}

	&__desc {
		margin-top: -.2em;
		margin-bottom: 1em;
		opacity: $opacity_normal;
		max-width: $maxWidth;
	}
}

</style>
