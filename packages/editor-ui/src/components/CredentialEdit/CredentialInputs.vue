<template>
	<div @keydown.stop :class="$style.container">
		<div v-for="parameter in credentialProperties" :key="parameter.name">
			<ParameterInputExpanded
				:parameter="parameter"
				:value="credentialData[parameter.name]"
				:documentationUrl="documentationUrl"
				:showValidationWarnings="showValidationWarnings"
				@change="valueChanged"
			/>
		</div>
	</div>
</template>

<script lang="ts">
import Vue from 'vue';

import { IUpdateInformation } from '../../Interface';

import ParameterInputExpanded from '../ParameterInputExpanded.vue';

export default Vue.extend({
	name: 'CredentialsInput',
	props: [
		'credentialProperties',
		'credentialData', // ICredentialsDecryptedResponse
		'documentationUrl',
		'showValidationWarnings',
	],
	components: {
		ParameterInputExpanded,
	},
	methods: {
		valueChanged(parameterData: IUpdateInformation) {
			const name = parameterData.name.split('.').pop();

			this.$emit('change', {
				name,
				value: parameterData.value,
			});
		},
	},
});
</script>

<style lang="scss" module>
.container {
	> * {
		margin-bottom: var(--spacing-l);
	}
}
</style>
