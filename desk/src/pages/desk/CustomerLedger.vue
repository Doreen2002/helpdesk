<template>
	<div class = "flex flex-col h-full px-4 overflow-hidden">
		<div class="flex flex-row py-10 px-8">
	<h1 class="text-blue-700 px-8 py-4">Add  filters</h1>
	<select class="block w-64 h-8 p-2 mb-6 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
		<option>Customer</option>
	</select>
	<span class="py-4 px-4">Equals</span>
	<input type="text" class="h-8 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-64 p-2.5  dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="filters">
	<button class="h-8 w-64 bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" @click="getGeneralLedger">Filter</button>
		</div>
	
		<div>
		<div class="grid grid-cols-12 gap-2">
			<div class="col-span-1">Posting Date</div>
			<div class="col-span-2">Account</div>
			<div class="col-span-1">Debit</div>
			<div class="col-span-1">Credit</div>
			<div class="col-span-1">Against</div>
			<div class="col-span-1">Party Type</div>
			<div class="col-span-1">Party</div>
			<div class="col-span-1">Against Voucher Type</div>
			<div class="col-span-1">Voucher Type</div>
			<div class="col-span-2">Voucher No</div>
			<template v-for="row in ledgerData" :key="row.name">
			<div class="col-span-1">{{ row.posting_date }}</div>
			<div class="col-span-2">{{ row.account }}</div>
			<div class="col-span-1">{{ row.debit }}</div>
			<div class="col-span-1" >{{ row.credit }}</div>
			<div class="col-span-1">{{ row.against }}</div>
			<div class="col-span-1">{{ row.party_type }}</div>
			<div class="col-span-1">{{ row.party }}</div>
			<div class="col-span-1">{{ row.against_voucher_type}}</div>
			<div class="col-span-1">{{ row.voucher_type }}</div>
			<div class="col-span-2">{{ row.voucher_no }}</div>
			</template>
			</div>
		</div>
			
			
		</div>

  </template>
  
  <script>

import ListManager from "@/components/global/ListManager.vue"
  export default {
    name: "GeneralLedger",
    data() {
        return {
            ledgerData: []
        };
    },
	methods: {
		getGeneralLedger: function()
		{
		fetch(`http://${window.location.hostname}:${ window.location.port}/api/resource/GL Entry/?fields=["posting_date","company","account", "party_type", "party", "debit","credit", "against", "against_voucher_type", "against_voucher", "voucher_type", "voucher_no"]&&filters={"party":"${this.filters}"}`, { method: "GET", headers: {
                "Authorization": "token 88a44253a62631a:cd57aa6393d60a0",
            },
        })
            .then(response => response.json())
            .then(data => {
            console.log(data.data);
            this.ledgerData = data.data;
        })
            .catch(error => console.error(error));

		}
	},
    mounted() {
        
    },
   
}
  </script>
  
  
 