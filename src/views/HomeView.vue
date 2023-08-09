<template>
  <div>
    <!-- <v-card class="main-card">
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Category ID"
          single-line
          hide-details
        ></v-text-field>
 
    </v-card> -->
    <v-row>
        <v-col>
          <v-select
            v-model="categories.id"
            :items="categories"
            item-text="name"
            item-value="id"
            label="filter Products By Category"
          ></v-select>
        </v-col>
        <v-col>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Find Product by ID"
            single-line
            hide-details
          ></v-text-field>
        </v-col>
    </v-row>
      <table>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>category_id</th>
        </tr>
        <tr v-for="(item, index) in selectedProducts" :key="index">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.category_id }}</td>
        </tr>
      </table>
  </div>
</template>

<script>
export default {
  
  data(){
    return{
      search: '',
      products: [
        { id: 1, name: 'Dell', category_id: 101 },
        { id: 2, name: 'Power Supply', category_id: 102 },
        { id: 3, name: 'Macbook', category_id: 101 },
        { id: 4, name: 'Monitor', category_id: 103 },
        { id: 5, name: 'Keyboard', category_id: 104 },
        { id: 6, name: 'Mouse', category_id: 104 },
        { id: 7, name: 'Headphones', category_id: 105 },
      ],
      categories: [
        { id: 101, name: 'Computers' },
        { id: 102, name: 'Power Supplies' },
        { id: 103, name: 'Monitors' },
      ],
    };
  },

  computed: {
    selectedProducts() {

      if (this.categories.id){

        const sortedProducts = this.products.filter(product => product.category_id === this.categories.id);
        sortedProducts.sort((a, b) => a.name.localeCompare(b.name));
        return sortedProducts;
      }

      if (this.search) {
        const sortedProducts = this.products.filter(product => product.id.toString() === this.search);
        return sortedProducts;
      }

      return this.products;
    },

  },
}


</script>

<style>

</style>
