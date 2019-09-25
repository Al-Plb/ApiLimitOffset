<template>
    <div class="q-pa-md">
      <div class="row justify-start">
        <div class="col-4 q-pa-xs">
          <q-input outlined  v-model="limit" dense @input="fetchData()"/>
        </div>
        <div class="col-4 q-pa-xs">
          <q-input outlined  v-model="offset" dense @input="fetchData()" />
        </div>
      </div>
      <ul>
        <li v-for="(info, index) in infos" :key="index">{{info.info.name}}</li>
      </ul>
      

    </div>

    <!-- items?limit=20&offset=200 -->
</template>

<script>
export default {
  name:'ApiResult',
  data: function() {
    return {
      infos: [],
      limit: 10,
      offset: 0,
      dense: true
    }
  },
  computed: {
    url : function() {
      return "https://api.cmdb-uat.corp.org.ebrc.local/items?limit="+ this.limit +"&offset=" + this.offset
    }
  },
  mounted() {
    this.fetchData();
  }, 
  methods: {
    fetchData() {
      this.axios.get(this.url)
      .then(response => {
        //console.log(response.data.data);
        this.infos = response.data.data;
      });
    }
  }
};
//https://api.cmdb-uat.corp.org.ebrc.local/items?limit="+ limit +"&offset=" + offset
</script>
