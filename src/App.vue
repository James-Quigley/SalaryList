<template>
  <div id="app">
    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <label class="input-group-text" for="inputGroupSelect01">Year</label>
      </div>
      <select v-model="year" class="custom-select" id="inputGroupSelect01">
        <option value="asu2017" selected>2017</option>
        <option value="asu2016">2016</option>
        <option value="asu2015">2015</option>
        <option value="asu2014">2014</option>
        <option value="asu2013">2013</option>
        <option value="asu2012">2012</option>
      </select>
    </div>
    <v-client-table v-if="getData != null" :data="getData" :columns="columns" :options="options"></v-client-table>
  </div>
</template>

<script>
import salaryData from "./data";

export default {
    name: "app",
    components: {},
    data: function() {
        return {
            salaryData,
            year: "asu2017",
            tableData: this.getData,
            columns: ["first_name", "last_name", "title", "salary"],
            options: {
                sortIcon: {
                    base: "fas",
                    up: "fa-sort-up",
                    down: "fa-sort-down",
                    is: "fa-sort"
                },
                headings: {
                    first_name: "First",
                    last_name: "Last",
                    title: "Title",
                    salary: "Salary"
                },
                sortable: ["first_name", "last_name", "title", "salary"],
                filterable: ["first_name", "last_name", "title"],
                customSorting: {
                    salary: function(ascending) {
                        return function(a, b) {
                            a = parseInt(
                                a.salary
                                    .substring(1, a.salary.length)
                                    .split(",")
                                    .join("")
                            );
                            b = parseInt(
                                b.salary
                                    .substring(1, b.salary.length)
                                    .split(",")
                                    .join("")
                            );

                            if (ascending) return a >= b ? 1 : -1;

                            return a <= b ? 1 : -1;
                        };
                    }
                }
            }
        };
    },
    methods: {},
    computed: {
        getData() {
            return salaryData[this.year];
        }
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /* margin-top: 60px; */
}

.input-group-text,
.VueTables__search-field > label,
.VueTables__limit-field > label {
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    padding: 0.375rem 0.75rem;
    margin-bottom: 0;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    text-align: center;
    white-space: nowrap;
    background-color: #e9ecef;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
}

.custom-select,
.VueTables__search-field > input,
.VueTables__limit-field > select {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
}
</style>
