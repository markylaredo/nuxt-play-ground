<template>

  <v-app>
      <v-main>
        <v-container><Nuxt /></v-container>
      </v-main>
    </v-app>
</template>
<script>
export default {

   head() {
    return {
    title: 'Nuxt play ground 🤪',

    }
  },
  methods:{
     downloadPdf() {
      this.$refs.html2Pdf.generatePdf();
    },
  }
}
</script>


<style >
table {
  border-collapse: collapse;
  width: 100%;
}

th,
td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

th {
  background-color: #4caf50;
  color: white;
}

tr:hover {
  background-color: #f5f5f5;
}

table input,
table input[type="text"],
table input[type="password"],
table input[type="email"] {
  display: block;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}

table input[type="text"]:focus,
table input[type="password"]:focus,
table input[type="email"]:focus {
  border: 1px solid #555;
  outline: none;
}


input,
input[type="text"],
input[type="password"],
input[type="email"] {
  display: block;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  transition: all 0.3s ease;
}

input[type="text"]:focus,
input[type="password"]:focus,
input[type="email"]:focus {
  border: 1px solid #555;
  outline: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
}

input[type="text"]:disabled,
input[type="password"]:disabled,
input[type="email"]:disabled {
  background-color: #f1f1f1;
  color: #888;
  cursor: not-allowed;
}

button {
  display: inline-block;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: none;
  border-radius: 4px;
  background-color: #4CAF50;
  color: white;
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover,
button:focus {
  background-color: #45a049;
}

button:active {
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
}

button:disabled {
  background-color: #ccc;
  color: #888;
  cursor: not-allowed;
}


select {
  display: block;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  background-color: #fff;
  transition: all 0.3s ease;
}

select:focus {
  border: 1px solid #555;
  outline: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
}

select:disabled {
  background-color: #f1f1f1;
  color: #888;
  cursor: not-allowed;
}

option {
  padding: 12px 20px;
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  background-color: #fff;
  color: #000;
}




</style>