<template>
  <div class="hello">
    <h1>Таблица</h1>
    <select v-model="selected">
      <option disabled value="">Выберите один из вариантов</option>
      <option v-for="reason in reasons" v-bind:value="reason.id">
          {{ reason.name }}
      </option>
      <option v-bind:value=-1>Вся таблица</option>
    </select>
    <br>
    <br>
    <table border="1">
      <template v-for="r in reasons">
        <template v-if="r.id==selected || selected==-1">
          <tr> 
              <td v-bind:rowspan="r.conds.length">{{r.name}}</td>
              <td>{{getConditionName(r.conds[0])}}</td>
          </tr>
          <template v-for="(k, index) in r.conds">
            <tr v-if="index > 0"> 
                <td>{{getConditionName(k)}}</td>
            </tr>
          </template>
        </template>
      </template>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
    conditions: [
      { id: 1, name: 'Condition 1'},
      { id: 2, name: 'Condition 2'},
      { id: 3, name: 'Condition 3'}
    ],
    reasons: [
      { id: 1, name: 'Reason 1', conds:[1,2] },
      { id: 2, name: 'Reason 2', conds:[2] },
      { id: 3, name: 'Reason 3', conds:[2,3] },
    ],
    selected: ''
    }
    
  },
  methods: {
    getConditionName: function(id){
      for(var i = 0;i < this._data.conditions.length; i++) {
        if (this._data.conditions[i].id == id) {
          return this._data.conditions[i].name;
        }
      }
    }
  },
  props: {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
      margin: auto;
      border-collapse: collapse;
}
TH, TD {
    border: 1px solid black; 
    text-align: center; 
    padding: 10px; 
   }
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
