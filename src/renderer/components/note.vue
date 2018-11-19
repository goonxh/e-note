<template>
  <div id="wrapper">
    <h3>nedb test</h3>
    <el-button size="small" @click="insert">insert</el-button>
    <el-button size="small" @click="find">find</el-button>

    <div>
      <ul>
        <li v-for="item in findData" :key="item._id">{{item._id}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  const Datastore = require('nedb');
  const db = new Datastore({filename: './data/note.db'});

  export default {
    data() {
      return{
        findData:[],
      }
    },
    created() {
      db.loadDatabase();
    },
    methods: {
      insert() {
        db.insert({
          name: 'test'
        }, (err, ret) => {
          if(err) console.log(err);
          this.find();
        });
      },
      find() {
        db.find({},(err, data) => {
          if(err) console.log(err);
          this.findData = data;
        })
      }
    }
  }
</script>

<style>
 
</style>
