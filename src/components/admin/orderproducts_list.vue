<template>
    
    <v-container style="width: 1000px; margin-left: 330px;">
        <!-- Pending Orders table -->
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>Order List</v-card-title>
              <!-- Replace with your insert component -->
              <insert @data-saved="getOrder" />
              <v-data-table 
                :headers="headers"
                :items="approvedOrders"
                item-key="id"
              >
              <template v-slot:[`item.transaction_code`]="{ item }">
                  <span>{{ item.transaction_code }}</span>
                </template>
                <template v-slot:[`item.updated_at`]="{ item }">
                  <span>{{ item.updated_at }}</span>
                </template>
                <template v-slot:[`item.created_at`]="{ item }">
                  <span>{{ item.created_at }}</span>
                </template>
                <template v-slot:[`item.image`]="{ item }">
                  <img :src="item.image" alt="Product Image" width="50" height="50">
                </template>
                <template v-slot:[`item.actions`]="{ item }">
                  <!-- <v-btn @click="pendingEvent(item.id)" color="error" small>
                    Undo
                  </v-btn> -->
                  <v-btn @click="deliveringEvent(item.id)" color="success" small>
                    Deliver Product
                  </v-btn>
                  <v-btn @click="openviewdialog(item.id)" color="black" small> <v-icon>mdi-eye</v-icon>
                    View Details
                  </v-btn>
                </template>
                <template v-for="(header, index) in headers" v-slot:[`header.${header.value}`]="{ props }">
                  <th :key="index">
                    <span>{{ getHeaderTitle(header.value) }}</span>
                  </th>
                </template>
              </v-data-table>
            </v-card>
          </v-col>
        </v-row>
    
        <!-- Approved Orders table -->
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>On Delivery Orders</v-card-title>
              <v-data-table
                :headers="headers"
                :items="deliveringOrders"
                item-key="id"
              >
              <template v-slot:[`item.transaction_code`]="{ item }">
                  <span>{{ item.transaction_code }}</span>
                </template>
                <template v-slot:[`item.updated_at`]="{ item }">
                  <span>{{ item.updated_at }}</span>
                </template>
                <template v-slot:[`item.created_at`]="{ item }">
                  <span>{{ item.created_at }}</span>
                </template>
                <template v-slot:[`item.image`]="{ item }">
                  <img :src="item.image" alt="Product Image" width="50" height="50">
                </template>
                <template v-slot:[`item.actions`]="{ item }">
                  <v-btn @click="approveEvent(item.id)" color="error" small>
                    Undo
                  </v-btn>
                  <v-btn @click="delivered(item.id)" color="success" small>
                    Item Delivered
                  </v-btn>
                  <v-btn @click="openviewdialog(item.id)" color="black" small> <v-icon>mdi-eye</v-icon>
                    View Details
                  </v-btn>
                </template>
                <template v-for="(header, index) in headers" v-slot:[`header.${header.value}`]="{ props }">
                  <th :key="index">
                    <span>{{ getHeaderTitle(header.value) }}</span>
                  </th>
                </template>
              </v-data-table>
            </v-card>
          </v-col>
        </v-row>
    
        <!-- Declined Orders table -->
        <v-row>
          <v-col>
            <v-card>
              <v-card-title>Delivered Orders</v-card-title>
              <v-data-table
                :headers="headers"
                :items="deliveredOrders"
                item-key="id"
              >
              <template v-slot:[`item.transaction_code`]="{ item }">
                  <span>{{ item.transaction_code }}</span>
                </template>
                <template v-slot:[`item.updated_at`]="{ item }">
                  <span>{{ item.updated_at }}</span>
                </template>
                <template v-slot:[`item.created_at`]="{ item }">
                  <span>{{ item.created_at }}</span>
                </template>
                <template v-slot:[`item.image`]="{ item }">
                  <img :src="item.image" alt="Product Image" width="50" height="50">
                </template>
                <template v-slot:[`item.actions`]="{ item }">
                  <v-btn @click="deliveringEvent(item.id)" color="success" small>
                    Undo
                  </v-btn>
                  <v-btn @click="openviewdialog(item.id)" color="black" small> <v-icon>mdi-eye</v-icon>
                    View Details
                  </v-btn>
                </template>
                <template v-for="(header, index) in headers" v-slot:[`header.${header.value}`]="{ props }">
                  <th :key="index">
                    <span>{{ getHeaderTitle(header.value) }}</span>
                  </th>
                </template>
              </v-data-table>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </template>
    
    <script>
    import axios from 'axios'; // Import axios library
    
    export default {
      data() {
        return {
          headers: [
            { text: 'Transaction Code', value: 'transaction_code' }, 
            { text: 'Date Updated', value: 'updated_at' }, 
            { text: 'Date Requested', value: 'created_at' }, 
            { text: 'Image', value: 'image' },
            { text: 'Product Name', value: 'prod_name' },
            { text: 'Unit Price', value: 'unit_price' },
            { text: 'Total', value: 'total' },
            { text: 'Size ID', value: 'size_id' },
            { text: 'Quantity', value: 'quantity' },
            { text: 'Address', value: 'address' },
            { text: 'Contact', value: 'contact' },
            { text: 'Other Info', value: 'other_info' },
            { text: 'Customer Name', value: 'customerName' },
            { text: 'Status', value: 'status' },
            { text: 'Actions', value: 'actions', sortable: false },
          ],
          infos: [] // Initialize infos as an empty array
        };
      },
      created() {
        this.getOrder();
      },
      computed: {
        approvedOrders() {
          return this.infos.filter(order => order.status !== 'pending' && order.status !== 'denied' && order.status !== 'delivering' && order.status !== 'recieved' && order.status !== 'cancelled' && order.status !== 'cancel' && order.status !== 'cart' && order.status !== 'deleted' && order.status !== 'pendingbackpricestock');
        },
        pendingOrders() {
          return this.infos.filter(order => order.status === 'pending');
        },
        deliveringOrders() {
          return this.infos.filter(order => order.status === 'delivering');
        },
        deliveredOrders() {
          return this.infos.filter(order => order.status === 'recieved');
        }
      },
      methods: {
        async getOrder() {
          try {
            const response = await axios.get('getOrder');
            this.infos = response.data; // Update this.infos instead of this.info
          } catch (error) {
            console.error(error);
          }
        },
        async approveEvent(id) {
      try {
        const response = await axios.post(`/updateOrderStatus/${id}`, { status: 'approved' });
        if (response.status === 200) {
          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } catch (error) {
        console.error('Error updating order status:', error);
      }
    },

    async delivered(id) {
      try {
        const response = await axios.post(`/updateOrderStatus/${id}`, { status: 'recieved' });
        if (response.status === 200) {
          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } catch (error) {
        console.error('Error updating order status:', error);
      }
    },
    
    
    async pendingEvent(id) {
      try {
        const response = await axios.post(`/updateOrderStatus/${id}`, { status: 'pending' });
        if (response.status === 200) {
          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } catch (error) {
        console.error('Error updating order status:', error);
      }
    },

     
    async deliveringEvent(id) {
      try {
        const response = await axios.post(`/updateOrderStatus/${id}`, { status: 'delivering' });
        if (response.status === 200) {
          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } catch (error) {
        console.error('Error updating order status:', error);
      }
    },
    async denyEvent(id) {
      try {
        const response = await axios.post(`/updateOrderStatus/${id}`, { 
          status: 'denied',
          reason: 'The Admin declined your order due to some reasons'
        });
        if (response.status === 200) {

          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } catch (error) {
        console.error('Error updating order status:', error);
      }
    },
  
        getHeaderTitle(field) {
          const headerTitles = {
            transaction_code: 'Transact Code',
            updated_at: 'Last Updated',
            created_at: 'Date Requested',
            image: 'Image',
            prod_name: 'Product Name',
            unit_price: 'Unit Price',
            total: 'Total Price',
            size_id: 'Size ID',
            quantity: 'Quantity',
            address: 'Address',
            contact: 'Contact',
            other_info: 'Other Info',
            customerName: 'Customer Name',
            status: 'Status',
            actions: 'Actions',
            
            // Add other field titles accordingly
          };
          return headerTitles[field] || '';
        },
      },
    };
    </script>
    
    <style>
    
    </style>
    