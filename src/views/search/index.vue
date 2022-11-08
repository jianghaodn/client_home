<template>
  <div class="page_search">
	<div class="warp">
	  <div class="container">
		<div class="row">
		  <div class="col-12">
			<div class="card_result_search">
			  <div class="title">搜索结果</div>
				<!-- 文章搜索结果 -->
			  <list_result_search
				:list="result_article"
				title="商城资讯"
				source_table="article"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/product_information/list', 'get')"
				:list="result_product_information_trade_name"
				title="商品信息商品名称"
				source_table="product_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/product_information/list', 'get')"
				:list="result_product_information_commodity_type"
				title="商品信息商品类型"
				source_table="product_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/order_information/list', 'get')"
				:list="result_order_information_user_name"
				title="订单信息用户姓名"
				source_table="order_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/order_information/list', 'get')"
				:list="result_order_information_trade_name"
				title="订单信息商品名称"
				source_table="order_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/distribution_information/list', 'get')"
				:list="result_distribution_information_user_name"
				title="配送信息用户姓名"
				source_table="distribution_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/distribution_information/list', 'get')"
				:list="result_distribution_information_trade_name"
				title="配送信息商品名称"
				source_table="distribution_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/return_information/list', 'get')"
				:list="result_return_information_order_number"
				title="退货信息订单编号"
				source_table="return_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/return_information/list', 'get')"
				:list="result_return_information_user_name"
				title="退货信息用户姓名"
				source_table="return_information"
			  ></list_result_search>
			  <list_result_search
				v-if="$check_action('/return_information/list', 'get')"
				:list="result_return_information_trade_name"
				title="退货信息商品名称"
				source_table="return_information"
			  ></list_result_search>
			</div>
		  </div>
		</div>
	  </div>
	</div>
  </div>
</template>

<script>
import mixin from "../../mixins/page.js";
import list_result_search from "../../components/diy/list_result_search.vue";

export default {
  mixins: [mixin],
  data() {
	return {
	  "query": {
		word: "",
	  },
	  "result_article": [],
			"result_product_information_trade_name":[],
			"result_product_information_commodity_type":[],
			"result_order_information_user_name":[],
			"result_order_information_trade_name":[],
			"result_distribution_information_user_name":[],
			"result_distribution_information_trade_name":[],
			"result_return_information_order_number":[],
			"result_return_information_user_name":[],
			"result_return_information_trade_name":[],
	};
  },
  methods: {
	/**
	 * 获取文章
	 */
	get_article() {
	  this.$get("~/api/article/get_list?like=0", { page: 1, size: 10, title: this.query.word }, (json) => {
		if (json.result) {
		  this.result_article = json.result.list;
		}
	  });
	},
	/**
	 * 获取trade_name
	 */
	get_product_information_trade_name(){
		this.$get("~/api/product_information/get_list?like=0", { page: 1, size: 10, "trade_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_product_information_trade_name = json.result.list;
			result_product_information_trade_name.map(o => o.title = o['trade_name'])
	  			this.result_product_information_trade_name = result_product_information_trade_name
		 	}
		});
	},
	/**
	 * 获取commodity_type
	 */
	get_product_information_commodity_type(){
		this.$get("~/api/product_information/get_list?like=0", { page: 1, size: 10, "commodity_type": this.query.word }, (json) => {
		  if (json.result) {
			var result_product_information_commodity_type = json.result.list;
			result_product_information_commodity_type.map(o => o.title = o['commodity_type'])
	  			this.result_product_information_commodity_type = result_product_information_commodity_type
		 	}
		});
	},
	/**
	 * 获取user_name
	 */
	get_order_information_user_name(){
		this.$get("~/api/order_information/get_list?like=0", { page: 1, size: 10, "user_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_order_information_user_name = json.result.list;
			result_order_information_user_name.map(o => o.title = o['user_name'])
	  			this.result_order_information_user_name = result_order_information_user_name
		 	}
		});
	},
	/**
	 * 获取trade_name
	 */
	get_order_information_trade_name(){
		this.$get("~/api/order_information/get_list?like=0", { page: 1, size: 10, "trade_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_order_information_trade_name = json.result.list;
			result_order_information_trade_name.map(o => o.title = o['trade_name'])
	  			this.result_order_information_trade_name = result_order_information_trade_name
		 	}
		});
	},
	/**
	 * 获取user_name
	 */
	get_distribution_information_user_name(){
		this.$get("~/api/distribution_information/get_list?like=0", { page: 1, size: 10, "user_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_distribution_information_user_name = json.result.list;
			result_distribution_information_user_name.map(o => o.title = o['user_name'])
	  			this.result_distribution_information_user_name = result_distribution_information_user_name
		 	}
		});
	},
	/**
	 * 获取trade_name
	 */
	get_distribution_information_trade_name(){
		this.$get("~/api/distribution_information/get_list?like=0", { page: 1, size: 10, "trade_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_distribution_information_trade_name = json.result.list;
			result_distribution_information_trade_name.map(o => o.title = o['trade_name'])
	  			this.result_distribution_information_trade_name = result_distribution_information_trade_name
		 	}
		});
	},
	/**
	 * 获取order_number
	 */
	get_return_information_order_number(){
		this.$get("~/api/return_information/get_list?like=0", { page: 1, size: 10, "order_number": this.query.word }, (json) => {
		  if (json.result) {
			var result_return_information_order_number = json.result.list;
			result_return_information_order_number.map(o => o.title = o['order_number'])
	  			this.result_return_information_order_number = result_return_information_order_number
		 	}
		});
	},
	/**
	 * 获取user_name
	 */
	get_return_information_user_name(){
		this.$get("~/api/return_information/get_list?like=0", { page: 1, size: 10, "user_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_return_information_user_name = json.result.list;
			result_return_information_user_name.map(o => o.title = o['user_name'])
	  			this.result_return_information_user_name = result_return_information_user_name
		 	}
		});
	},
	/**
	 * 获取trade_name
	 */
	get_return_information_trade_name(){
		this.$get("~/api/return_information/get_list?like=0", { page: 1, size: 10, "trade_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_return_information_trade_name = json.result.list;
			result_return_information_trade_name.map(o => o.title = o['trade_name'])
	  			this.result_return_information_trade_name = result_return_information_trade_name
		 	}
		});
	},

  },
  components: { list_result_search },
	created(){
    this.query.word = this.$route.query.word || "";
  },
  mounted() {
	this.get_article();
		this.get_product_information_trade_name();
		this.get_product_information_commodity_type();
		this.get_order_information_user_name();
		this.get_order_information_trade_name();
		this.get_distribution_information_user_name();
		this.get_distribution_information_trade_name();
		this.get_return_information_order_number();
		this.get_return_information_user_name();
		this.get_return_information_trade_name();
  },
  watch: {
	$route() {
	  $.push(this.query, this.$route.query);
	  this.get_article();
	  this.get_product_information_trade_name();
	  this.get_product_information_commodity_type();
	  this.get_order_information_user_name();
	  this.get_order_information_trade_name();
	  this.get_distribution_information_user_name();
	  this.get_distribution_information_trade_name();
	  this.get_return_information_order_number();
	  this.get_return_information_user_name();
	  this.get_return_information_trade_name();
	},
  },
};
</script>

<style scoped>
.card_search {
  text-align: center;
}
.card_result_search>.title {
  text-align: center;
  padding: 10px 0;
}
</style>
