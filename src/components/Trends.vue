<template>
	<div class="bricklayer" ref="bricklayer">
	  <div v-for="data in datas">
	  	<a :to="data.url" :href="data.url" target="_blank">
	  		<img class="brick-img" :src="'https://media.giphy.com/media/' + data.id + '/giphy.gif'">
	  	</a>
	  </div>
	</div>
</template>

<script>
import Bricklayer from 'bricklayer';
import '../assets/bricklayer.min.css';

export default {
	name: 'trends',
	props: [
		'page',
		'search',
	],
	data() {
		return {
			datas: {},
	    	limit: 25,
	    	offset: this.page,
		}
	},
	created() {
		this.fetchTrends({
			limit: this.limit,
			offset: this.offset
		});
	},
	mounted() {
		this.brickLayerInit();
	},
	watch: {
		page() {
			this.fetchTrends({
				offset: this.page
			})
			//this.brickLayerInit();
			scrollTo(document.body, 0, 1250);
		},
		search() {
			this.searchTrends({
				offset: this.page,
				search: this.search
			})
		}
	},
	methods: {
		fetchTrends(data) {
			let api_key = this.$store.state.API_KEY;
			let endpoint = this.$store.state.endpoints.trending;
			let limit = this.limit;
			let offset = this.offset + data.offset;

			fetch(`${endpoint}?api_key=${api_key}&limit=${limit}&offset=${offset}`, {
				method: 'GET',
			}).then((resp) => {
				return resp.json();
			}).then((obj) => {
				this.datas = obj.data;
			})

		},
		searchTrends(data) {
			let api_key = this.$store.state.API_KEY;
			let endpoint = this.$store.state.endpoints.search;
			let limit = this.limit;
			let offset = this.offset + data.offset;
			let search = data.search;

			fetch(`${endpoint}?api_key=${api_key}&q=${search}&limit=${limit}&offset=${offset}`, {
				method: 'GET',
			}).then((resp) => {
				return resp.json();
			}).then((obj) => {
				this.datas = obj.data;
			})
		},
		brickLayerInit() {
			var bricklayer = null;

			setTimeout(() => {
				bricklayer = new Bricklayer(this.$refs.bricklayer)
			}, 1000);

		},
		scrollTo(element, to, duration) {
		    var start = element.scrollTop,
		        change = to - start,
		        currentTime = 0,
		        increment = 20;
		        
		    var animateScroll = function(){        
		        currentTime += increment;
		        var val = this.easeInOutQuad(currentTime, start, change, duration);
		        element.scrollTop = val;
		        if(currentTime < duration) {
		            setTimeout(animateScroll, increment);
		        }
		    };
		    animateScroll();
		},
		easeInOutQuad(t, b, c, d) {
		  t /= d/2;
			if (t < 1) return c/2*t*t + b;
			t--;
			return -c/2 * (t*(t-2) - 1) + b;
		}
	}
}
</script>

<style scoped>
	.bricklayer {
		margin-bottom: 20px;
	}
	.brick-img {
		width: 100%;
	}
</style>
