<template>
  
   <!-- Approved Request Table -->
   <div style="height:1000px;">
   <v-col cols="12" style="margin-left: 350px; width:940px;">
    <br><br><br><br><br><br><br>
    <v-row>
      <v-col>
        <v-select v-model="selectedOption" :items="options" label="Select Table" style=" position:absolute; right:73px; width:200px;top:7%;" outlined></v-select>
      </v-col>
    </v-row>
    <v-card v-if="selectedOption === 'Pending Request'">
     <v-card-title >
       <h2 style="color:#1679AB; font-size:25px;">Pending Requests</h2>
     </v-card-title>
     <v-card-text>
       <v-data-table
       
         :headers="tableHeaders"
         :items="pendingRequests"
         item-key="event_title"
         :items-per-page="10"
       >
         
       <template v-slot:[`item.event_title`]="{ item }">
         {{ item.event_title }}
       </template>
       <template v-slot:[`item.start_date`]="{ item }">
         {{ item.start_date }}
       </template>
       <template v-slot:[`item.end_date`]="{ item }">
         {{ item.end_date }}
       </template>
       <template v-slot:[`item.location`]="{ item }">
         {{ item.location }}
       </template>
       <template v-slot:[`item.event_description`]="{ item }">
         {{ item.event_description }}
       </template>
       <template v-slot:[`item.name`]="{ item }">
         {{ item.name }}
       </template>
       <template v-slot:[`item.email`]="{ item }">
         {{ item.email }}
       </template>
       <template v-slot:[`item.phone`]="{ item }">
         {{ item.phone }}
       </template>
       <template v-slot:[`item.service`]="{ item }">
         {{ item.service }}
       </template>
       <template v-slot:[`item.status`]="{ item }">
         {{ item.status }}
       </template>
       <template v-slot:[`item.actions`]="{ item }">
         <v-btn small color="success" @click="viewEvent(item)">
           <v-icon>mdi-eye</v-icon>
           View
         </v-btn>
         <!-- Add other action buttons here -->
       </template>
       </v-data-table>
     </v-card-text>
   </v-card>
 </v-col>


   <!-- Approved Request Table -->
   <v-col cols="12" style="margin-top:-30px;margin-left: 350px; width:935px;">
    <v-card v-if="selectedOption === 'Approved Request'">
    <v-card-title>
      <h2 style="color:#1679AB; font-size:25px;">Approved Requests</h2>
    </v-card-title>
    <v-card-text>
      <v-data-table
        :headers="tableHeaders"
        :items="approvedRequests"
        item-key="event_title"
        :items-per-page="10"
      >
        
      <template v-slot:[`item.event_title`]="{ item }">
        {{ item.event_title }}
      </template>
      <template v-slot:[`item.start_date`]="{ item }">
        {{ item.start_date }}
      </template>
      <template v-slot:[`item.end_date`]="{ item }">
        {{ item.end_date }}
      </template>
      <template v-slot:[`item.location`]="{ item }">
        {{ item.location }}
      </template>
      <template v-slot:[`item.event_description`]="{ item }">
        {{ item.event_description }}
      </template>
      <template v-slot:[`item.name`]="{ item }">
        {{ item.name }}
      </template>
      <template v-slot:[`item.email`]="{ item }">
        {{ item.email }}
      </template>
      <template v-slot:[`item.phone`]="{ item }">
        {{ item.phone }}
      </template>
      <template v-slot:[`item.service`]="{ item }">
        {{ item.service }}
      </template>
      <template v-slot:[`item.status`]="{ item }">
        {{ item.status }}
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-btn small color="success" @click="viewEvent(item)">
          <v-icon>mdi-eye</v-icon>
          View
        </v-btn>
        <!-- Add other action buttons here -->
      </template>
      </v-data-table>
    </v-card-text>
  </v-card>
</v-col>


  <!-- Declined Request Table -->
  <v-col cols="12" style="margin-top:-30px; margin-left: 350px; width:940px;">
    <v-card v-if="selectedOption === 'Declined Request'">
    <v-card-title>
      <h2 style="color:#1679AB; font-size:25px;">Declined Requests</h2>
    </v-card-title>
    <v-card-text>
      <v-data-table
        :headers="tableHeaders"
        :items="declinedRequests"
        item-key="event_title"
        :items-per-page="10"
      >
       
      <template v-slot:[`item.event_title`]="{ item }">
        {{ item.event_title }}
      </template>
      <template v-slot:[`item.start_date`]="{ item }">
        {{ item.start_date }}
      </template>
      <template v-slot:[`item.end_date`]="{ item }">
        {{ item.end_date }}
      </template>
      <template v-slot:[`item.location`]="{ item }">
        {{ item.location }}
      </template>
      <template v-slot:[`item.event_description`]="{ item }">
        {{ item.event_description }}
      </template>
      <template v-slot:[`item.name`]="{ item }">
        {{ item.name }}
      </template>
      <template v-slot:[`item.email`]="{ item }">
        {{ item.email }}
      </template>
      <template v-slot:[`item.phone`]="{ item }">
        {{ item.phone }}
      </template>
      <template v-slot:[`item.service`]="{ item }">
        {{ item.service }}
      </template>
      <template v-slot:[`item.status`]="{ item }">
        {{ item.status }}
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-btn small color="success" @click="viewEvent(item)">
          <v-icon>mdi-eye</v-icon>
          View
        </v-btn>
        <!-- Add other action buttons here -->
      </template>
      </v-data-table>
    </v-card-text>
  </v-card>
</v-col>


<v-dialog v-model="showModal" max-width="800px">
  <v-card>
    <v-toolbar color="primary" dark>
      <v-btn icon @click="closeModal">
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-toolbar-title>{{ selectedEvent.event_title }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <!-- Neumorphic Approve Button -->
      <v-btn text color="white" @click="approveEvent">Approve</v-btn>
      <v-btn text color="white" @click="declineEvent">Decline</v-btn>
    </v-toolbar>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-row v-for="(value, key) in selectedEvent" :key="key">
              <!-- Check if the key is not 'id' before displaying it -->
              <template v-if="key !== 'id'">
                <v-col cols="12">
                  <span>{{ formatLabel(key) }}:</span>
                </v-col>
                <v-col cols="12">
                  <v-text-field v-model="selectedEvent[key]" readonly outlined></v-text-field>
                </v-col>
              </template>
            </v-row>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
  </v-card>
</v-dialog>



</div>
  


</template>

<script>
import axios from 'axios';
import emailjs from 'emailjs-com';

export default {
  data() {
    return {
      showModal: false,
      selectedEvent: {}, // Holds the selected event details
      info: [],
      selectedOption: 'Pending Request', // Default selected option
      options: ['Pending Request', 'Approved Request', 'Declined Request'], // Dropdown options
      tableHeaders: [
        { text: 'Action', value: 'actions', sortable: false },
        { text: 'Event', value: 'event_title' },
        { text: 'Start Date', value: 'start_date' },
        { text: 'End Date', value: 'end_date' },
        { text: 'Location', value: 'location' },
        { text: 'Event Description', value: 'event_description' },
        { text: 'Contact Name', value: 'name' },
        { text: 'Email', value: 'email' },
        { text: 'Phone Number', value: 'phone' },
        { text: 'Type of Service', value: 'service' },
        { text: 'Status', value: 'status' },
      ],
    };
  },
  computed: {
    pendingRequests() {
      return this.info.filter(item => item.status !== 'approved' && item.status !== 'declined' && item.status !== 'done');
    },
    approvedRequests() {
      return this.info.filter(item => item.status === 'approved');
    },
    declinedRequests() {
      return this.info.filter(item => item.status === 'declined');
    },
    showPendingtable() {
      return this.pendingRequests.length > 0;
    },
    showApprovedTable() {
      return this.approvedRequests.length > 0;
    },
    showDeclinedTable() {
      return this.declinedRequests.length > 0;
    },
  },
  created() {
    this.getEventInfo();
  },
  methods: {
    formatDate(date) {
      return new Date(date).toLocaleDateString(); // Adjust date formatting as needed
    },
    async approveEvent() {
      try {
        const response = await axios.post('/updateEventStatus', {
          id: this.selectedEvent.id,
          status: 'approved'
        });

        if (response.status === 200) {
          // Update the status in the selectedEvent object
          this.selectedEvent.status = 'approved';
          this.getEventInfo();

          // Find the index of the updated event in the info array and update it
          const index = this.info.findIndex(event => event.id === this.selectedEvent.id);
          if (index !== -1) {
            this.$set(this.info, index, { ...this.selectedEvent });
          }

          this.showModal = false; // Close the modal

          // Send email notification
          this.sendApprovalEmail();
        } else {
          console.error('Error updating event status');
        }
      } catch (error) {
        console.error('Error updating event status:', error);
      }
    },
    async declineEvent() {
      try {
        const response = await axios.post('/updateEventStatus', {
          id: this.selectedEvent.id,
          status: 'declined',
          reason: 'The Admin declined your order due to some reasons'
        });

        if (response.status === 200) {
          // Update the status in the selectedEvent object
          this.selectedEvent.status = 'declined';
          this.getEventInfo();
          this.showModal = false; // Close the modal after approval

          // Find the index of the updated event in the info array and update it
          const index = this.info.findIndex(event => event.id === this.selectedEvent.id);
          if (index !== -1) {
            this.$set(this.info, index, { ...this.selectedEvent });
          }

          this.showModal = false;
        } else {
          console.error('Error updating event status');
        }
      } catch (error) {
        console.error('Error updating event status:', error);
      }
    },
    viewEvent(item) {
      // Set the selected event when "View" button is clicked
      this.selectedEvent = { ...item }; // Copy the item details to selectedEvent
      this.showModal = true; // Open the modal
    },
    closeModal() {
      this.showModal = false; // Close the modal
    },
    formatLabel(key) {
      // Convert camelCase to Title Case for labels
      return key.replace(/([a-z])([A-Z])/g, '$1 $2').toUpperCase();
    },
    async getEventInfo() {
      try {
        const response = await axios.get('getevent');
        this.info = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    sendApprovalEmail() {
      const templateParams = {
        to_email: this.selectedEvent.email,
        from_email: 'rence.quinio12@gmail.com',
        subject: 'Event Approval Notification',
        message: 'Your event has been approved.'
      };

      emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams, 'YOUR_USER_ID')
        .then((response) => {
          console.log('Email sent successfully!', response.status, response.text);
        }, (error) => {
          console.error('Failed to send email:', error);
        });
    }
  }
};
</script>

<style>

</style>


