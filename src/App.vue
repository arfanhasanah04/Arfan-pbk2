<template>
  <div id="app">
    <h1>List Harga Barang</h1>
    
    <!-- Form untuk memasukkan pengeluaran baru -->
    <form @submit.prevent="addExpense">
      <label for="description">Nama barang:</label>
      <input type="text" id="description" v-model="newExpense.description" required>

      <label for="amount">Harga:</label>
      <input type="number" id="amount" v-model.number="newExpense.amount" required>

      <button type="submit">tambahkan</button>
    </form>

    <!-- Daftar pengeluaran -->
    <div class="expenses">
      <h2>List</h2>
      <ul>
        <li v-for="(expense, index) in expenses" :key="index" :class="{ 'highlight': expense.amount > limit }">
          <span class="description">{{ expense.description }}</span> 
          <span class="amount">{{ formatRupiah(expense.amount) }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newExpense: {
        description: '',
        amount: ''
      },
      expenses: [],
      limit: 50000 // Batas pengeluaran untuk penyorotan
    };
  },
  methods: {
    addExpense() {
      this.expenses.push({...this.newExpense});
      this.newExpense.description = '';
      this.newExpense.amount = '';
    },
    formatRupiah(amount) {
      return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(amount);
    }
  }
};
</script>

<style scoped>
/* General styles */
body {
  font-family: 'Montserrat', sans-serif; /* Menggunakan font Montserrat */
  margin: 0;
  padding: 0;
  background-color: #c1e90e; /* Mengubah latar belakang menjadi hijau */
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #1adee8;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-family: 'Montserrat', sans-serif; /* Menggunakan font Montserrat */
}

form {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-bottom: 20px;
}

form label {
  width: 100px;
}

form input {
  flex: 1;
  padding: 8px;
  margin-bottom: 10px;
}

form button {
  background-color: #e1eb29;
  color: #010300;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

form button:hover {
  background-color: #e51310;
}

.expenses {
  background-color: #faf0f0;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

.expenses h2 {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
  font-family: 'Montserrat', sans-serif; /* Menggunakan font Montserrat */
}

.expenses ul {
  list-style: none;
  padding: 0;
}

.expenses li {
  border-bottom: 1px solid #9c464600;
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.expenses li:last-child {
  border-bottom: none;
}

.expenses .highlight {
  color: rgb(255, 0, 0);
}

.expenses .description {
  flex: 1;
}

.expenses .amount {
  font-weight: bold;
}
</style>
