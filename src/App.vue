<template>

	  <div class="wrapper">
		  <h1>Список тегов</h1>
		  <p>Ниже 5 блоков у которых разная ширина, в них вложен компонент TagsList (у него никаких ограничений по ширине и высоте нет)</p>
		  <p>Отображается ровно столько тегов, сколько поместилось полностью (На ресайз не делал)</p>

		  <div class="sm">
			  <tags-list :list="list" align="center"/>
		  </div>
		  <div class="md">
			  <tags-list :list="list" align="center"/>
		  </div>
		  <div class="bg">
			  <tags-list :list="list" align="center"/>
		  </div>
		  <div class="lg">
			  <tags-list :list="list" align="center"/>
		  </div>
		  <div>
			  <tags-list :list="list" align="center"/>
		  </div>
	  </div>

</template>

<script>
import TagsList from './components/TagsList';

export default {
  name: 'App',
  components: {
	  TagsList,
  },

	data() {
	  return {
		  list: [
			  {
				  name: '123',
				  icon: 'mdi-domain',
			  },
			  {
				  name: 'название 2',
			  },
			  {
				  name: 'название 3',
				  icon: 'mdi-lifebuoy',
			  },
			  {
				  name: 'название 4',
				  icon: 'mdi-desktop-classic',
			  },
			  {
				  name: 'название 5',
				  icon: 'mdi-domain',
			  },
			  {
				  name: 'название 6',
				  icon: 'mdi-dropbox',
			  },

		  ]
	  }
	}
};
</script>

<style lang="scss" scoped>
	.wrapper {
	  max-width: 1400px;
	  margin: 0 auto;
	}

	.sm {
	  max-width: 300px;
	}
	.md {
	  max-width: 400px;
	}

	.bg {
	  max-width: 550px;
	}

	.lg {
	  max-width: 700px;
	}

	div {
	  border: 1px solid;
	}
</style>
