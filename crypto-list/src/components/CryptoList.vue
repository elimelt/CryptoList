<template>
    <div>
      <div class="mode-select">
        <input type="radio" id="search" value="search" v-model="mode">
        <label for="search">Search</label>
        <input type="radio" id="sort" value="sort" v-model="mode">
        <label for="sort">Sort</label>
      </div>
      <div v-if="mode === 'search'" class="search-container">
        <input type="text" v-model="search" placeholder="Search">
      </div>
      <div v-else class="sort-container">
        <select v-model="sortOrder">
          <option value="asc">Ascending</option>
          <option value="desc">Descending</option>
        </select>
      </div>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Symbol</th>
            <th>Price (USD)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="crypto in filteredCryptos" :key="crypto.id">
            <td>{{ crypto.name }}</td>
            <td>{{ crypto.symbol }}</td>
            <td>{{ Math.round(100000*crypto.priceUsd)/100000.0 }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        cryptos: [],
        search: '',
        mode: 'search',
        sortOrder: 'asc',
      };
    },
    computed: {
      filteredCryptos() {
        let filtered = [];

        if (this.mode === 'search') {
          filtered = this.cryptos.filter((crypto) => {
            return crypto.name.toLowerCase().includes(this.search.toLowerCase());
          });
        } else {
          filtered = [...this.cryptos];
          filtered.sort((a, b) => {
            if (this.sortOrder == 'asc') {
              return parseFloat(a.priceUsd) - parseFloat(b.priceUsd);
            } else {
              return b.priceUsd - a.priceUsd;
            }
          });
        }

        return filtered;
      },
    },
    mounted() {
      axios
        .get('https://api.coincap.io/v2/assets')
        .then((response) => {
          this.cryptos = response.data.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  };
  </script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  padding: 10px;
  text-align: left;
  background-color: #213857;
  border-bottom: 1px solid #ccc;
}

th {
  background-color: #04193a;
  font-weight: 800;
  font-size: 30px;
}

td {
  font-size: 18px;
}

.mode-select {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
  }

  .mode-select input[type="radio"] {
    display: none;
  }

  .mode-select label {
    font-size: 16px;
    margin-right: 20px;
    cursor: pointer;
  }

  .mode-select input[type="radio"]:checked + label {
    font-weight: bold;
  }

  .search-container,
  .sort-container {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .search-container input[type="text"],
  .sort-container select {
    background-color: rgb(218, 235, 250);
    padding: 10px;
    font-size: 16px;
    border: 1px solid gray;
    border-radius: 5px;
    margin-right: 20px;
  }
</style>

  