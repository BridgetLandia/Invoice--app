<template>
  <div>
    <v-card color="#f5eee8">
      <div>
        <h1 id="main_title">Invoice App</h1>
        <h3 id="subtitle">InvoiceTea for your invoice Team</h3>
      </div>
      <v-form d-flex>
        <v-card class="ma-12 pa-16" raised elevation="12">
          <v-row>
            <h2 id="invoice_title">Invoice</h2>
          </v-row>
          <v-row justify="center">
            <v-col md="4">
              <h3>FROM:</h3>
              <label for="Businesss Name">Businesss Name</label>
              <v-text-field label="Solo" placeholder="Business Name" solo></v-text-field>
              <label for="Tax Number">Tax Number</label>
              <v-text-field label="Solo" placeholder="Tax Number" solo></v-text-field>
              <label for="Address Line 1">Address Line 1</label>
              <v-text-field label="Solo" placeholder="Address Line 1" solo></v-text-field>
              <label for="Address Line 2">Address Line 2</label>
              <v-text-field label="Solo" placeholder="Address Line 2" solo></v-text-field>
              <label for="City">City</label>
              <v-text-field label="Solo" placeholder="City" solo></v-text-field>
              <label for="Postcode">PostCode</label>
              <v-text-field label="Solo" placeholder="Postcode" solo></v-text-field>
            </v-col>
            <v-col md="4">
              <h3>TO:</h3>
              <label for="Businesss Name">Businesss Name</label>
              <v-text-field label="Solo" placeholder="Business Name" solo></v-text-field>
              <label for="Tax Number">Tax Number</label>
              <v-text-field label="Solo" placeholder="Tax Number" solo></v-text-field>
              <label for="Address Line 1">Address Line 1</label>
              <v-text-field label="Solo" placeholder="Address Line 1" solo></v-text-field>
              <label for="Address Line 2">Address Line 2</label>
              <v-text-field label="Solo" placeholder="Address Line 2" solo></v-text-field>
              <label for="City">City</label>
              <v-text-field label="Solo" placeholder="City" solo></v-text-field>
              <label for="Postcode">PostCode</label>
              <v-text-field label="Solo" placeholder="Postcode" solo></v-text-field>
            </v-col>
            <v-col md="4">
              <h3>Details:</h3>
              <label for="Invoice Number">Invoice Number</label>
              <v-text-field label="Solo" placeholder="Invoice Number" solo></v-text-field>
              <label for="Issue Date">Issue Date</label>
              <v-text-field label="Solo" placeholder="Issue Date" solo></v-text-field>
              <label for="Issue Date">Purchase Order Number</label>
              <v-text-field label="Solo" placeholder="PO Number" solo></v-text-field>
              <label for="Due Date">Due Date</label>
              <v-text-field label="Solo" placeholder="Due Date" solo></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col md="12">
              <h3>Items:</h3>
              <thead>
                <tr>
                  <th class="text-left">No.</th>
                  <th class="text-left">Desciption</th>
                  <th class="text-left">Qty</th>
                  <th class="text-left">Price</th>
                  <th class="text-left">Discount</th>
                  <th class="text-left">Tax</th>
                  <th class="text-left">Total</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in items" :key="index">
                  <td>{{ index +1 }}</td>
                  <td>
                    <v-text-field label="Solo" placeholder="Description" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Qty" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Price" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Discount" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Tax" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Total" solo></v-text-field>
                  </td>
                  <td>
                    <v-btn small color="primary">Add</v-btn>
                    <v-btn small color="primary">Remove</v-btn>
                  </td>
                </tr>
                <tr>
                  <td>Discount:</td>
                </tr>
                <tr>
                  <td>Tax:</td>
                </tr>
                <tr>
                  <td>Total:</td>
                </tr>
              </tbody>
            </v-col>
          </v-row>
          <v-row>
            <v-col md="4">
              <h3>Bank Information:</h3>
              <label for="Invoice Number">Bank Name</label>
              <v-text-field label="Solo" placeholder="Bank Name" solo></v-text-field>
              <label for="Issue Date">Account number</label>
              <v-text-field label="Solo" placeholder="02213425" solo></v-text-field>
              <label for="Due Date">SWIFT Code</label>
              <v-text-field label="Solo" placeholder="SWIFT" solo></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <label for="Invoice Notes">Invoice Notes</label>
              <v-textarea solo name="input-7-4" label="Solo textarea"></v-textarea>
            </v-col>
          </v-row>
        </v-card>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "invoice",
  data() {
    return {
      businessName: "",
      from_address1: "",
      from_address2: "",
      from_city: "",
      from_postcode: "",
      clientName: "",
      client_address1: "",
      client_address2: "",
      client_city: "",
      client_postcode: "",
      invoice_id: "",
      invoice_date: "",
      invoice_due: "",
      items: [
        {
          description: "",
          qty: "",
          price: "",
          discount: "",
          tax: "",
          discount_amount: "",
          tax_amount: "",
          total: "",
        },
      ],
    };
  },
};
</script>

<style scoped>
#main_title {
  padding: 2rem;
}
#invoice_title {
  font-size: 3rem;
  padding-left: 2rem;
  padding-bottom: 4rem;
}
#subtitle {
  margin-left: 2rem;
}
</style>