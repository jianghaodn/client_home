<template>
	<div class="diy_edit page_order_information" id="order_information_edit">
		<div class='warp'>
			<div class='container'>
				<div class='row diy_edit_content_box'>
					<div v-if="$check_field('set','order_number') || $check_field('add','order_number') || $check_field('get','order_number')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>订单编号:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_order_number" v-model="form['order_number']" placeholder="请输入订单编号" v-if="(form['order_number'] && $check_field('set','order_number')) || (!form['order_number'] && $check_field('add','order_number'))" :disabled="true"/>
							<span v-else-if="$check_field('get','order_number')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','purchase_user') || $check_field('add','purchase_user') || $check_field('get','purchase_user')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>购买用户:
							</span>
						</div>
						<div class="diy_field diy_down">
							<select id="form_purchase_user" :disabled="disabledObj['purchase_user_isDisabled']" v-model="form['purchase_user']" v-if="(form['purchase_user'] && $check_field('set','purchase_user')) || (!form['purchase_user'] && $check_field('add','purchase_user'))" >
								<option v-for="o in list_user_purchase_user" :value="o['user_id']">
									{{o['nickname'] + '-' + o['username']}}
								</option>
							</select>
							<span v-else-if="$check_field('get','purchase_user')">{{ form['purchase_user'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','user_name') || $check_field('add','user_name') || $check_field('get','user_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>用户姓名:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_user_name" v-model="form['user_name']" placeholder="请输入用户姓名" v-if="(form['user_name'] && $check_field('set','user_name')) || (!form['user_name'] && $check_field('add','user_name'))"  :disabled="disabledObj['user_name_isDisabled']"/>
							<span v-else-if="$check_field('get','user_name')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','subscriber_telephone') || $check_field('add','subscriber_telephone') || $check_field('get','subscriber_telephone')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>用户电话:
							</span>
						</div>
						<!-- 手机 -->
						<div class="diy_field diy_phone">
							<input type="tel" id="form_subscriber_telephone" v-model="form['subscriber_telephone']" placeholder="请输入用户电话" v-if="(form['subscriber_telephone'] && $check_field('set','subscriber_telephone')) || (!form['subscriber_telephone'] && $check_field('add','subscriber_telephone'))" :disabled="disabledObj['subscriber_telephone_isDisabled']" />
							<span v-else-if="$check_field('get','subscriber_telephone')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','user_address') || $check_field('add','user_address') || $check_field('get','user_address')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>用户地址:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_user_address" v-model="form['user_address']" placeholder="请输入用户地址" v-if="(form['user_address'] && $check_field('set','user_address')) || (!form['user_address'] && $check_field('add','user_address'))"  :disabled="disabledObj['user_address_isDisabled']"/>
							<span v-else-if="$check_field('get','user_address')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','trade_name') || $check_field('add','trade_name') || $check_field('get','trade_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>商品名称:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_trade_name" v-model="form['trade_name']" placeholder="请输入商品名称" v-if="(form['trade_name'] && $check_field('set','trade_name')) || (!form['trade_name'] && $check_field('add','trade_name'))"  :disabled="disabledObj['trade_name_isDisabled']"/>
							<span v-else-if="$check_field('get','trade_name')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','commodity_price_') || $check_field('add','commodity_price_') || $check_field('get','commodity_price_')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>商品价钱:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_commodity_price_" v-model="form['commodity_price_']" placeholder="请输入商品价钱" v-if="(form['commodity_price_'] && $check_field('set','commodity_price_')) || (!form['commodity_price_'] && $check_field('add','commodity_price_'))"  :disabled="disabledObj['commodity_price__isDisabled']"/>
							<span v-else-if="$check_field('get','commodity_price_')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','purchase_quantity') || $check_field('add','purchase_quantity') || $check_field('get','purchase_quantity')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>购买数量:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_purchase_quantity" v-model="form['purchase_quantity']" placeholder="请输入购买数量" v-if="(form['purchase_quantity'] && $check_field('set','purchase_quantity')) || (!form['purchase_quantity'] && $check_field('add','purchase_quantity'))"  :disabled="disabledObj['purchase_quantity_isDisabled']"/>
							<span v-else-if="$check_field('get','purchase_quantity')">{{ form['user_name'] }}</span>
						</div>
					</div>
					<div v-if="$check_field('set','total') || $check_field('add','total') || $check_field('get','total')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>总计:
							</span>
						</div>
						<!-- 文本 -->
						<div class="diy_field diy_text">
							<input type="text" id="form_total" v-model="form['total']" placeholder="请输入总计" v-if="(form['total'] && $check_field('set','total')) || (!form['total'] && $check_field('add','total'))"  @focus="set_total()" :disabled="disabledObj['total_isDisabled']"/>
							<span v-else-if="$check_field('get','total')">{{ form['user_name'] }}</span>
						</div>
					</div>
				</div>
				<div class="diy_edit_submit_box row">
					<div class="col-12">
						<div class="btn_box">
							<button class="btn_submit" @click="submit()">提交</button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import mixin from "@/mixins/page.js";
	export default {
		mixins: [mixin],
		components: {},
		data() {
			return {
				url_get_obj: "~/api/order_information/get_obj?",
				url_add: "~/api/order_information/add?",
				url_set: "~/api/order_information/set?",

				// 登录权限
				oauth: {
					"signIn": true,
					"user_group": []
				},

				// 查询条件
				query: {
					"order_number": "",
					"purchase_user": 0,
					"user_name": "",
					"subscriber_telephone": "",
					"user_address": "",
					"trade_name": "",
					"commodity_price_": "",
					"purchase_quantity": "",
					"total": "",
					"order_information_id": 0,
				},

				obj: {
					"order_number":this.$get_stamp(), // 订单编号
					"purchase_user": 0, // 购买用户
					"user_name":'', // 用户姓名
					"subscriber_telephone":'', // 用户电话
					"user_address":'', // 用户地址
					"trade_name":'', // 商品名称
					"commodity_price_":'', // 商品价钱
					"purchase_quantity":'', // 购买数量
					"total":'', // 总计
					"order_information_id": 0,
				},

				// 表单字段
				form: {
					"order_number":this.$get_stamp(), // 订单编号
					"purchase_user": 0, // 购买用户
					"user_name":'', // 用户姓名
					"subscriber_telephone":'', // 用户电话
					"user_address":'', // 用户地址
					"trade_name":'', // 商品名称
					"commodity_price_":'', // 商品价钱
					"purchase_quantity":'', // 购买数量
					"total":'', // 总计
					"order_information_id": 0,

				},
				disabledObj:{
					"order_number_isDisabled": false,
					"purchase_user_isDisabled": false,
					"user_name_isDisabled": false,
					"subscriber_telephone_isDisabled": false,
					"user_address_isDisabled": false,
					"trade_name_isDisabled": false,
					"commodity_price__isDisabled": false,
					"purchase_quantity_isDisabled": false,
					"total_isDisabled": false,
				},
				// 用户列表
				list_user_purchase_user: [],

				// ID字段
				field: "order_information_id",
			}
		},
		methods: {
			/**
			 * 获取普通用户用户列表
			 */
			async get_list_user_purchase_user() {
				// if(this.user_group !== "管理员" && this.form["purchase_user"] === 0) {
				//     this.form["purchase_user"] = this.user.user_id;
				// }
				var json = await this.$get("~/api/user/get_list?user_group=普通用户");
				if(json.result && json.result.list){
					this.list_user_purchase_user = json.result.list;
				}
				else if(json.error){
					console.error(json.error);
				}
			},
			async get_user_session_purchase_user(){
				var _this = this;
				var json = await this.$get("~/api/user_group/get_obj?name=普通用户");
				if(json.result && json.result.obj){
					var source_table = json.result.obj.source_table;
					var user_id = _this.$store.state.user.user_id;
					if (user_id){
						var url = "~/api/"+source_table+"/get_obj?"
						this.$get(url, {"user_id":_this.$store.state.user.user_id}, function(res) {
							if (res.result && res.result.obj) {
								var arr = []
								for (let key in res.result.obj) {
									arr.push(key)
								}
								var arrForm = []
								for (let key in _this.form) {
									arrForm.push(key)
								}
								_this.form["purchase_user"] = user_id
								_this.disabledObj['purchase_user' + '_isDisabled'] = true
								for (var i=0;i<arr.length;i++){
									for (var j=0;j<arrForm.length;j++){
										if (arr[i]===arrForm[j]){
											if (arr[i]!=="purchase_user") {
												_this.form[arrForm[j]] = res.result.obj[arr[i]]
												_this.disabledObj[arrForm[j] + '_isDisabled'] = true
												break;
											}
										}
									}
								}
							}
						});
					}
				}
				else if(json.error){
					console.error(json.error);
				}
			},
			set_total(){
				this.form.total =this.form.commodity_price_ * this.form.purchase_quantity
			},

			/**
			 * 修改文件
			 * @param { Object } files 上传文件对象
			 * @param { String } str 表单的属性名
			 */
			change_file(files, str) {
				var form = new FormData();
				form.append("file", files[0]);
				this.$post("~/api/order_information/upload?", form, (res) => {
					if (res.result) {
						this.form[str] = res.result.url;
					} else if (res.error) {
						this.$toast(res.error.message);
					}
				});
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_before(param){
				var form = $.db.get("form");
				if (form) {
					this.obj = $.push(this.obj ,form);
					this.form = $.push(this.form ,form);
				}
				var arr = []
				for (let key in form) {
					arr.push(key)
				}
				for (var i=0;i<arr.length;i++){
					this.disabledObj[arr[i] + '_isDisabled'] = true
				}
				return param;
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_after(json ,func){
				var form = $.db.get("form");
				var obj = Object.assign({} ,form ,this.obj);
				if (form) {
					this.obj = $.push(this.obj ,obj);
				}
				if (form) {
					this.form = $.push(this.form ,form);
				}
				if(func){
					func(json);
				}
			},

		},
		created() {
			this.get_user_session_purchase_user();
			this.get_list_user_purchase_user();
		}
	}
</script>

<style>
</style>
