<script >
  import axios from 'axios'
 
 export default {
     data(){
         return {
             students: [],
         }
         
     },	 
     mounted: function(){
         axios.get("http://34.82.81.113:3000/students").then((response)=>{
             console.log(response.data);
             this.students = response.data;
         })
     },
     methods: {
     },
 }
</script>

<template>
  <table class="table">
    <thead class="bg-orange-100">
				<tr>
					<td>ПІБ</td>
					<td>Група</td>
					<td>Оцінка</td>
					<td>Наявність роботи</td>
				</tr>
			</thead>
			<tbody class="">
				<tr v-for="st in students" :key="st._id">
					<td><router-link :to="'/student-info/'+st._id" v-if="update!=st._id">{{st.name}}</router-link><input type="text" :value="st.name" @input="st.name=$event.target.value" v-else></td>
					<td><span v-if="update!=st._id">{{st.group}}</span>
						<select id="select" v-model="st.group" v-else>
							<option value="RPZ 19 1/9">RPZ 19 1/9</option>
							<option value="RPZ 19 2/9">RPZ 19 2/9</option>
						</select>
					</td>
					<td><span v-if="update!=st._id">{{st.mark}}</span><input type="text" :value="st.mark" @input="st.mark=$event.target.value" v-else></td>
					<td><input type="checkbox" v-model="st.isDonePr" disabled v-if="update!=st._id"><input type="checkbox" v-model="st.isDonePr" v-else></td>
				</tr>
			</tbody>
  </table>
</template>

<style scoped>
.table {
  /* border: rgb(249, 115, 22) 1px; */
  @apply table-auto w-1/2 mr-auto ml-auto mt-20 border-collapse border-orange-500 border bg-yellow-50 
}
.table td{
  @apply border-orange-500 border
}
</style>
