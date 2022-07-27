<template>
	<ul class="tags-list" :class="classObject" ref="list">
		<li class="tags-item"  v-for="(tag, index) in list" :key="tag.id" ref="tag">
			<v-icon class="tags-divider" v-if="index > 0" v-text="'mdi-vector-point'"/>
			<v-icon class="tags-icon" v-if="tag.icon" v-text="tag.icon"/>
			<span class="tags-text" v-text="tag.name"/>
		</li>
	</ul>
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
			}
		},
		mounted() {
			const config = {
				root: this.$refs.list,
				threshold: 1
			};

			this.observer = new IntersectionObserver(function(entries) {
				entries.forEach(entry => {
					entry.target.style = entry.isIntersecting ? '' : 'visibility: hidden'
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
		padding: 30px 40px;
		display: flex;
		flex-wrap: nowrap;
		flex-shrink: 1;
	  }

      &-icon {
        margin-right: 10px;
      }

	  &-item {
		display: flex;
		align-items: center;
        flex-wrap: nowrap;
		flex-grow: 2;

		&:hover {
          cursor: pointer;
		  color: red;
		}
	  }

	  &-text {
		white-space: nowrap;
	  }

	  &-divider {
		padding: 0 40px;
		width: 10px;
		height: 10px;
	  }

	}

    .center {
      justify-content: space-between;
    }
</style>