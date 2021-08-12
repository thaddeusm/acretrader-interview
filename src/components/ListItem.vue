<template>
	<div class="card">
		<div class="card-header">
			<h6>{{ item.id }} by user {{ item.userId }}</h6>
			<h2>{{ item.title }}</h2>
		</div>
		<div class="card-body">
			<p v-if="item.completed">
				task complete
			</p>
			<p v-else>
				task incomplete
			</p>
			<button @click="handleClick">
				back
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ListItem',
	props: {
		item: Object
	},
	methods: {
		handleClick: function() {
			this.$emit('close-item-view');
		}
	}
}
</script>

<style scoped>
  .card {
    border: 1px solid black;
    margin: 1rem;
    padding: 10px;
  }

  .card-header {
    grid-area: header;
    text-align: left;
  }

  .card-body {
    grid-area: header;
    text-align: left;
  }
</style>