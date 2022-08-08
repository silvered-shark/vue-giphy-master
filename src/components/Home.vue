<template>
  <div>
  	<search :search="searchGif"></search>
  	<trends :page="page" :search="search"></trends>
  	<button class="loadMore" v-on:click="loadMore" ref="loadMore">Load More...</button>
  </div>
</template>

<script>
import Trends from './Trends';
import Search from './Search';

export default {
  name: 'home',
  data () {
    return {
    	page: 0,
    	search: '',
    }
  },
  components: {
  	Trends,
  	Search
  },
  mounted() {
  	document.querySelector("*").style.backgroundColor = this.getRandomColor();
  },
  methods: {
  	getRandomColor() {
  		let hex = Math.floor(Math.random() * 0xFFFFFF);
  		return "#" + ("000000" + hex.toString(16)).substr(-6);
  	},
  	loadMore() {
  		this.page += 25;
  	},
  	searchGif() {
  		let search = document.querySelector(".search").value;
  		this.search = search;
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.loadMore {
		cursor: pointer;
		margin-left: 30% !important;
		width: 40%;
		padding: 10px;
		background-color: black;
		border:1px solid #25729a; -webkit-border-radius: 3px; -moz-border-radius: 3px;border-radius: 3px;font-size:12px;
		border-bottom: 4px solid #294452;
		font-family:arial, helvetica, sans-serif; padding: 10px 10px 10px 10px; text-decoration:none; display:inline-block;
		text-shadow: -1px -1px 0 rgba(0,0,0,0.3);font-weight:bold; color: #FFFFFF;
		background-color: #3093c7; background-image: -webkit-gradient(linear, left top, left bottom, from(#3093c7), to(#1c5a85));
		background-image: -webkit-linear-gradient(top, #3093c7, #1c5a85);
		background-image: -moz-linear-gradient(top, #3093c7, #1c5a85);
		background-image: -ms-linear-gradient(top, #3093c7, #1c5a85);
		background-image: -o-linear-gradient(top, #3093c7, #1c5a85);
	}
	.loadMore:hover {
		border:1px solid #1c5675;
		border-bottom: 4px solid #294452;
 		background-color: #26759e; background-image: -webkit-gradient(linear, left top, left bottom, from(#26759e), to(#133d5b));
		background-image: -webkit-linear-gradient(top, #26759e, #133d5b);
		background-image: -moz-linear-gradient(top, #26759e, #133d5b);
		background-image: -ms-linear-gradient(top, #26759e, #133d5b);
		background-image: -o-linear-gradient(top, #26759e, #133d5b);
	}
</style>
