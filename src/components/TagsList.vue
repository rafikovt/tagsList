<template>
	<div class="tags-list" :class="classObject" ref="list">
		<template v-for="(tag, index) in list">
			<v-icon class="tags-divider" v-if="index > 0" v-text="'mdi-vector-point'" />
			<span class="tags-item" :key="index" ref="tag">
				<v-icon class="tags-icon" v-if="tag.icon" v-text="tag.icon"/>
				<span class="tags-text" v-text="tag.name"/>
			</span>
		</template>
	</div>
</template>

<script>
	export default {
		name: 'tags-list',
		props: {
			list: {
				type: Array,
				required: true,
			},
			align: {
				type: String,
				required: false,
				default: 'start'
			},
		},
		data() {
			return {
				observer: null,
			}
		},
		computed: {
			classObject() {
				return {
					'center': this.align === 'center',
					'left': this.align === 'start',
				}
			},
		},
		mounted() {
			const config = {
				root: this.$refs.list,
				threshold: 1
			};

			this.observer = new IntersectionObserver(function(entries) {
				entries.forEach(entry => {
					if (entry.isIntersecting) {
						entry.target.style = ''
						if (entry.target.previousElementSibling) {
							entry.target.previousElementSibling.style =  ''
						}
					} else {
						entry.target.style =  'display: none'
						if (entry.target.previousElementSibling) {
							entry.target.previousElementSibling.style =  'display: none'
						}
					}

				});
			}, config);
			this.$refs.tag.forEach(e => this.observer.observe(e))
		},
		beforeDestroy() {
			this.$refs.tag.forEach(e => this.observer.unobserve(e))
		}
	}
</script>

<style lang="scss" scoped>
	.tags {
	  &-list {
		padding: 30px 20px;
		display: flex;
		align-items: center;
		flex-wrap: nowrap;
		flex-shrink: 1;
	  }

      &-icon {
        margin-right: 10px;
      }

	  &-item {
		padding: 0 20px;
		display: flex;
		align-items: center;
        flex-wrap: nowrap;

		&:hover {
          cursor: pointer;
		  color: red;
		}
	  }

	  &-text {
		white-space: nowrap;
	  }

	  &-divider {
		padding: 0 20px;
		width: 10px;
		height: 10px;
	  }

	}

    .center {
      justify-content: space-between;
    }
</style>