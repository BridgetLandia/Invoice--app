<template>
  <div>
    <v-card v-if="!showPreview" color="#f5eee8">
      <div id="title_container">
        <h1 id="main_title">Invoice App</h1>
        <img alt="logo" id="logo" src="../assets/teabag.svg" />
      </div>
      <h3 id="subtitle">InvoiceTea for your Invoice Team</h3>

      <v-form d-flex>
        <v-card class="ma-12 pa-16" raised elevation="12">
          <v-row>
            <h2 id="invoice_title">Invoice</h2>
          </v-row>
          <v-row justify="center">
            <v-col md="4">
              <h3>FROM:</h3>
              <label for="Businesss Name">Business Name</label>
              <v-text-field
                label="Solo"
                type="text"
                v-model.trim="businessName"
                placeholder="Business Name"
                solo
              ></v-text-field>
              <label for="Tax Number">Tax Number</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="from_taxnumber"
                placeholder="Tax Number"
                solo
              ></v-text-field>
              <label for="Address Line 1">Address Line 1</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="from_address1"
                placeholder="Address Line 1"
                solo
              ></v-text-field>
              <label for="Address Line 2">Address Line 2</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="from_address2"
                placeholder="Address Line 2"
                solo
              ></v-text-field>
              <label for="City">City</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="from_city"
                placeholder="City"
                solo
              ></v-text-field>
              <label for="Postcode">PostCode</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="from_postcode"
                placeholder="Postcode"
                solo
              ></v-text-field>
            </v-col>
            <v-col md="4">
              <h3>TO:</h3>
              <label for="Businesss Name">Business Name</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="clientName"
                placeholder="Business Name"
                solo
              ></v-text-field>
              <label for="Tax Number">Tax Number</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="client_taxnumber"
                placeholder="Tax Number"
                solo
              ></v-text-field>
              <label for="Address Line 1">Address Line 1</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="client_address1"
                placeholder="Address Line 1"
                solo
              ></v-text-field>
              <label for="Address Line 2">Address Line 2</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="client_address2"
                placeholder="Address Line 2"
                solo
              ></v-text-field>
              <label for="City">City</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="client_city"
                placeholder="City"
                solo
              ></v-text-field>
              <label for="Postcode">PostCode</label>
              <v-text-field
                type="text"
                label="Solo"
                v-model.trim="client_postcode"
                placeholder="Postcode"
                solo
              ></v-text-field>
            </v-col>
            <v-col md="4">
              <h3>Details:</h3>
              <label for="Invoice Number">Invoice Number</label>
              <v-text-field
                label="Solo"
                v-model.trim="invoice_id"
                placeholder="Invoice Number"
                solo
              ></v-text-field>
              <label for="Issue Date">Issue Date</label>
              <v-menu
                ref="menu1"
                v-model="menu1"
                :close-on-content-click="false"
                transition="scale-transition"
                offset-y
                max-width="290px"
                min-width="290px"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="dateFormatted"
                    solo
                    label="Date"
                    hint="MM/DD/YYYY format"
                    persistent-hint
                    v-bind="attrs"
                    @blur="date = parseDate(dateFormatted)"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker v-model="date" no-title @input="menu1 = false"></v-date-picker>
              </v-menu>
              <label for="Issue Date">Purchase Order Number</label>
              <v-text-field label="Solo" v-model.trim="purchase_order" placeholder="PO Number" solo></v-text-field>
              <label for="Due Date">Due Date</label>
              <v-menu
                ref="menu2"
                v-model="menu2"
                :close-on-content-click="false"
                transition="scale-transition"
                offset-y
                max-width="290px"
                min-width="200px"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="dateFormatted"
                    solo
                    label="Date"
                    hint="MM/DD/YYYY format"
                    persistent-hint
                    v-bind="attrs"
                    @blur="date = parseDate(dateFormatted)"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker v-model="date" no-title @input="menu2 = false"></v-date-picker>
              </v-menu>
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
                    <v-text-field
                      label="Solo"
                      placeholder="Description"
                      v-model="item.description"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Qty" v-model.number="item.qty" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field label="Solo" placeholder="Price" v-model.number="item.price" solo></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Discount"
                      v-model.number="item.discount_amount"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Tax"
                      v-model.number="item.tax_amount"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Total"
                      :value="item.total"
                      readonly
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-btn color="primary" class="button-remove" @click="removeItem(index)">Remove</v-btn>
                  </td>
                </tr>
                <tr>
                  <v-btn small color="primary" class="button-add" @click="addItem(index)">Add</v-btn>
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
              <v-text-field label="Solo" placeholder="Bank Name" v-model="bank_name" solo></v-text-field>
              <label for="Issue Date">Account number</label>
              <v-text-field label="Solo" placeholder="02213425" v-model="bank_account" solo></v-text-field>
              <label for="Due Date">SWIFT Code</label>
              <v-text-field label="Solo" placeholder="SWIFT" v-model="swift_code" solo></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <label for="Invoice Notes">Invoice Notes</label>
              <v-textarea solo name="input-7-4" v-model="invoice_notes" label="Solo textarea"></v-textarea>
            </v-col>
          </v-row>
          <v-btn @click="preview" color="primary">Preview</v-btn>
        </v-card>
      </v-form>
    </v-card>
    <!-- Invoice Template -->
    <div v-else>
      <v-navigation-drawer
        v-model="drawer"
        :color="color"
        :expand-on-hover="expandOnHover"
        :mini-variant="miniVariant"
        :right="right"
        :permanent="permanent"
        absolute
        dark
      >
        <v-list>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title>You Invoice</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item @click="printToPDF()" color="primary">Save PDF</v-list-item>
          <v-list-item @click="editInvoice" color="primary">Edit</v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-card class="ma-12 pa-16">
        <div id="invoice_template">
          <v-row justify="center">
            <v-col md="4">
              <h3>FROM</h3>
              <label class="labels" for="Businesss Name">Business Name:</label>
              <div>{{businessName}}</div>
              <label class="labels" for="Tax Number">Tax Number:</label>
              <div>{{from_taxnumber}}</div>
              <label class="labels" for="Address Line 1">Address Line 1:</label>
              <div>{{from_address1}}</div>
              <label class="labels" for="Address Line 2">Address Line 2:</label>
              <div>{{from_address2}}</div>
              <label class="labels" for="City">City:</label>
              <div>{{from_city}}</div>
              <label class="labels" for="Postcode">PostCode:</label>
              <div>{{from_postcode}}</div>
            </v-col>
            <v-col md="4">
              <h3>TO:</h3>
              <label class="labels" for="Businesss Name">Business Name</label>
              <div>{{clientName}}</div>
              <label class="labels" for="Tax Number">Tax Number</label>
              <div>{{client_taxnumber}}</div>
              <label class="labels" for="Address Line 1">Address Line 1</label>
              <div>{{client_address1}}</div>
              <label class="labels" for="Address Line 2">Address Line 2</label>
              <div>{{client_address2}}</div>
              <label class="labels" for="City">City</label>
              <div>{{client_city}}</div>
              <label class="labels" for="Postcode">PostCode</label>
              <div>{{client_postcode}}</div>
            </v-col>
            <v-col md="4">
              <h3>Details:</h3>
              <label class="labels" for="Invoice Number">Invoice Number</label>
              <div>{{invoice_id}}</div>
              <label class="labels" for="Issue Date">Issue Date</label>
              <div>{{invoice_date}}</div>
              <label class="labels" for="Issue Date">Purchase Order</label>
              <div>{{purchase_order}}</div>
              <label class="labels" for="Issue Date">Due Date</label>
              <div>{{invoice_due}}</div>
            </v-col>
          </v-row>
          <v-row>
            <v-col md="12">
              <h3>Items:</h3>
              <v-simple-table>
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
                    <td>{{item.description}}</td>
                    <td>{{item.qty}}</td>
                    <td>{{item.price}}</td>
                    <td>{{item.discount_amount}}</td>
                    <td>{{item.tax_amount}}</td>
                    <td>{{item.total}}</td>
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
              </v-simple-table>
            </v-col>
          </v-row>
          <v-row>
            <v-col md="4">
              <h3>Bank Information:</h3>
              <label for="Invoice Number">Bank Name</label>
              <div>{{bank_name}}</div>
              <label for="Issue Date">Account number</label>
              <div>{{bank_account}}</div>
              <label for="Due Date">SWIFT Code</label>
              <div>{{swift_code}}</div>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <label for="Invoice Notes">Invoice Notes</label>
              <div id="invoice_notes">{{invoice_notes}}</div>
            </v-col>
          </v-row>
        </div>
      </v-card>
    </div>
  </div>
</template>

<script>
import html2pdf from "html2pdf.js";
export default {
  name: "invoice",
  data() {
    return {
      businessName: "",
      from_taxnumber: "",
      from_address1: "",
      from_address2: "",
      from_city: "",
      from_postcode: "",
      clientName: "",
      client_taxnumber: "",
      client_address1: "",
      client_address2: "",
      client_city: "",
      client_postcode: "",
      invoice_id: "",
      invoice_date: "",
      purchase_order: "",
      invoice_due: "",
      items: [
        {
          description: "",
          qty: "",
          price: "",
          discount_amount: 0,
          tax_amount: 0,
          total: 0,
        },
      ],
      taxtotal: 0,
      total: 0,
      bank_name: "",
      bank_account: "",
      swift_code: "",
      invoice_notes: "",
      date: new Date().toISOString().substr(0, 10),
      dateFormatted: this.formatDate(new Date().toISOString().substr(0, 10)),
      menu1: false,
      menu2: false,
      showPreview: false,
      drawer: true,
      color: "blue",
      colors: ["primary", "blue", "success", "red", "teal"],
      right: true,
      permanent: true,
      miniVariant: false,
      expandOnHover: true,
      background: false,
    };
  },
  methods: {
    addItem(index) {
      this.items.splice(index + 1, 0, {
        description: "",
        qty: "",
        price: "",
        discount_amount: 0,
        tax_amount: 0,
        total: 0,
      });
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    formatDate(date) {
      if (!date) return null;

      const [year, month, day] = date.split("-");
      return `${month}/${day}/${year}`;
    },
    parseDate(date) {
      if (!date) return null;
      const [month, day, year] = date.split("/");
      return `${year}-${month.padStart(2, "0")}-${day.padStart(2, "0")}`;
    },
    printWindow: function () {
      const element = document.getElementById("invoice_template").innerHTML;
      document.body.innerHTML = element;
      window.print();
      window.location.reload();
    },
    printToPDF: function () {
      const element = document.getElementById("invoice_template");
      const opt = {
        margin: 10,
        filename: "invoice.pdf",
        image: { type: "jpeg", quality: 1 },
        html2canvas: { scale: 2, scrollX: 0, scrollY: 0 },
      };
      html2pdf().from(element).set(opt).save();
    },
    preview: function () {
      this.showPreview = true;
      window.scroll(0, 0);
    },
    editInvoice: function () {
      this.showPreview = false;
    },
  },
  computed: {
    computedDateFormatted() {
      return this.formatDate(this.date);
    },
  },
  watch: {
    date() {
      this.dateFormatted = this.formatDate(this.date);
      this.invoice_date = this.date;
    },
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
.button-remove {
  margin-bottom: 1.5rem;
}
.v-btn:not(.v-btn--round).v-size--default {
  height: 47px;
  min-width: 64px;
  padding: 0 16px;
}
#invoice_notes {
  border: 1px solid grey;
}
#title_container {
  display: flex;
  align-items: center;
}
#logo {
  height: 50px;
  position: relative;
  margin-left: -4rem;
  margin-top: 3.5rem;
}
.labels {
  font-weight: 700;
}
</style>