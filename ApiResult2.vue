<template>
    <div class="q-pa-md">
      <q-table 
        :data="infos"
        :columns="columns"
        row-key="name"
        :pagination.sync="infoPagination"
      >
      </q-table>
    </div>

</template>

<script>
export default {
  name:'ApiResult',
  data: function() {
    return {
      infoPagination: {
        page: 1,
        rowsNumber: 10
      },
      infos: [],
      columns: [
        {
          name: 'name',
          required: true,
          label: 'Name',
          align: 'center',
          field: row => row.name,
          sortable: true
        },
        { name: 'client', align: 'center', label: 'Client', field: "client"},
        { name: 'family',align: 'center', label: 'Family', field: "family"},
        { name: 'type', align: 'center', label: 'Type', field: "type"},
      ]
    }
  },
  computed: {
    url : function() {
      return "https://api.cmdb-uat.corp.org.ebrc.local/items?"
    }
  },
  mounted() {
    this.request({
      pagination: this.infoPagination
    })
  }, 
  methods: {
    request ({ infoPagination }) {

      // we do the server data fetch, based on pagination and filter received
      // (using Axios here, but can be anything; parameters vary based on backend implementation)

      this.axios.get(this.url)
      .then(({ data }) => {
        this.infos = data.data;
        // updating pagination to reflect in the UI
        this.infoPagination = pagination

        // we also set (or update) rowsNumber
        this.infoPagination.rowsNumber = data.rowsNumber

        // then we update the rows with the fetched ones
        this.infos = data.rows
        
      })
      .catch(error => {
        
      })
      
    }
    //https://api.cmdb-uat.corp.org.ebrc.local/items?limit="+ limit +"&offset=" + offset
  }
}
</script>










<template>
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="datas"
        :columns="columns"
        row-key="name"
      ></q-table>
      <p>{{datas.info}}</p>
    </div>

</template>

<script>
export default {
  name:'ApiResult',
  data: function() {
    return {
      columns: [
        {
          name: 'name',
          required: true,
          label: 'name',
          align: 'left',
          field: 'name',
          format: val => `${val}`,
          sortable: true
        },
        { name: 'client', align: 'center', label: 'client', field: 'client', sortable: true },
        { name: 'family', label: 'family', field: 'family', sortable: true },
        { name: 'type', label: 'type', field: 'type' },
      ],
      datas: []
      
    }
    
  },
  mounted() {
   this.fetchData();
  }, 
  methods: {
    fetchData() {
          this.axios.get("https://api.cmdb-uat.corp.org.ebrc.local/items?")
          .then(response => {
            console.log(response.data.data);
            this.datas = response.data.data;
          });
        }
    //https://api.cmdb-uat.corp.org.ebrc.local/items?limit="+ limit +"&offset=" + offset
  }
}
</script>




