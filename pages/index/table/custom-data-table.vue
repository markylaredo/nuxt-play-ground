<template>
  <div>
    <DataTable :columns="columns" :items="items" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      items: 
        [
          {
            id: 1,
            name: 'Alice',
            email: 'alice@example.com',
          },
          {
            id: 2,
            name: 'Bob',
            email: 'bob@example.com',
          },
          {
            id: 3,
            name: 'Carol',
            email: 'carol@example.com',
          },
          {
            id: 4,
            name: 'Dave',
            email: 'dave@example.com',
          },
          {
            id: 5,
            name: 'Eve',
            email: 'eve@example.com',
          },
          {
            id: 6,
            name: 'Frank',
            email: 'frank@example.com',
          },
          {
            id: 7,
            name: 'Grace',
            email: 'grace@example.com',
          },
          {
            id: 8,
            name: 'Heather',
            email: 'heather@example.com',
          },
          {
            id: 9,
            name: 'Ivan',
            email: 'ivan@example.com',
          },
          {
            id: 10,
            name: 'Judy',
            email: 'judy@example.com',
          },
          {
            id: 11,
            name: 'Karen',
            email: 'karen@example.com',
          },
          {
            id: 12,
            name: 'Larry',
            email: 'larry@example.com',
          },
          {
            id: 13,
            name: 'Mandy',
            email: 'mandy@example.com',
          },
          {
            id: 14,
            name: 'Nancy',
            email: 'nancy@example.com',
          },
          {
            id: 15,
            name: 'Oscar',
            email: 'oscar@example.com',
          },
          {
            id: 16,
            name: 'Patty',
            email: 'patty@example.com',
          },
          {
            id: 17,
            name: 'Quinn',
            email: 'quinn@example.com',
          },
          {
            id: 18,
            name: 'Randy',
            email: 'randy@example.com',
          },
          {
            id: 19,
            name: 'Sandy',
            email: 'sandy@example.com',
          },
          {
            id: 20,
            name: 'Tina',
            email: 'tina@example.com',
          },
        ],    
      columns: [
        { label: 'Name', key: 'name' },
        { label: 'Email', key: 'email' },
      ],
    }
  },
  mounted() {},
}
</script>
