<template>
  <v-card v-if="!showPreview" color="#f5eee8">
    <div id="title_container">
      <h1 id="main_title">Invoice App</h1>
    </div>
    <h3 id="subtitle">InvoiceTea for your Invoice Team</h3>

    <v-form d-flex>
      <v-card class="ma-12 pa-16" raised elevation="12">
        <v-row>
          <h2 id="invoice_title">Invoice</h2>
        </v-row>
        <v-row justify="center">
          <v-col md="4">
            <h3>From</h3>
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
            <v-text-field type="text" label="Solo" v-model.trim="from_city" placeholder="City" solo></v-text-field>
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
            <h3>To</h3>
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
            <h3>Details</h3>
            <label for="Invoice Number">Invoice Number</label>
            <v-text-field label="Solo" v-model.trim="invoice_id" placeholder="Invoice Number" solo></v-text-field>
            <label for="Issue Date">Purchase Order Number</label>
            <v-text-field label="Solo" v-model.trim="purchase_order" placeholder="PO Number" solo></v-text-field>
            <label for="Issue Date">Issue Date</label>
            <datepicker class="datepicker" v-model="invoice_date"></datepicker>
            <label for="Due Date">Due Date</label>
            <datepicker class="datepicker" v-model="invoice_due"></datepicker>
          </v-col>
        </v-row>
        <v-row>
          <v-col md="12">
            <h3>Items:</h3>
            <table>
              <thead>
                <tr>
                  <th class="text-left">No.</th>
                  <th class="text-left">Desciption</th>
                  <th class="text-left">Qty</th>
                  <th class="text-left">Price</th>
                  <th class="text-left">Discount %</th>
                  <th class="text-left">Discount Amount</th>
                  <th class="text-left">Tax %</th>
                  <th class="text-left">Tax Amount</th>
                  <th class="text-left">Total</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in items" :key="index">
                  <td width="10%" class="item-index">{{ index +1 }}</td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Description"
                      v-model="item.description"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Qty"
                      v-model.number="item.qty"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Price"
                      v-model.number="item.price"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Discount"
                      v-model.number="item.discount"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Discount"
                      v-model.number="item.discount_amount"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Tax"
                      v-model.number="item.tax"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      label="Solo"
                      placeholder="Tax"
                      v-model.number="item.tax_amount"
                      @blur="itemTotal(index)"
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-text-field
                      height="24px"
                      label="Solo"
                      placeholder="Total"
                      :value="item.total"
                      readonly
                      solo
                    ></v-text-field>
                  </td>
                  <td>
                    <v-btn color="primary" class="item-button" @click="removeItem(index)">
                      <v-icon>mdi-minus</v-icon>
                    </v-btn>
                  </td>
                  <td>
                    <v-btn color="primary" class="item-button" @click="addItem(index)">
                      <v-icon>mdi-plus</v-icon>
                    </v-btn>
                  </td>
                </tr>
              </tbody>
            </table>
            <table id="small-table">
              <tbody>
                <tr>
                  <td class="labels border_bottom">Discount:</td>
                  <td class="labels border_bottom">{{itemsDiscountTotal}}</td>
                </tr>
                <tr>
                  <td class="labels border_bottom">Tax:</td>
                  <td class="labels border_bottom">{{itemsTaxTotal}}</td>
                </tr>
                <tr>
                  <td class="labels border_bottom">Total:</td>
                  <td class="labels border_bottom">{{itemsTotal}}</td>
                </tr>
              </tbody>
            </table>
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
            <v-textarea solo name="input-7-4" v-model="invoice_notes" label="Something important"></v-textarea>
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
            <v-list-item-title>Your Invoice</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list-item-icon>
          <v-list-item @click="printWindow()" color="primary">
            <v-icon class="pdf-icon">{{ 'mdi-cloud-print-outline' }}</v-icon>
            <v-list-item-content>Print to PDF</v-list-item-content>
          </v-list-item>
        </v-list-item-icon>
        <v-list-item-icon>
          <v-list-item @click="printToPDF()" color="primary">
            <v-icon class="pdf-icon">{{ 'mdi-content-save-all' }}</v-icon>
            <v-list-item-content>Save PDF</v-list-item-content>
          </v-list-item>
        </v-list-item-icon>
        <v-list-item-icon>
          <v-icon>{{ 'mdi-square-edit-outline' }}</v-icon>
          <v-list-item @click="editInvoice" color="primary">
            <v-list-item-content>Edit</v-list-item-content>
          </v-list-item>
        </v-list-item-icon>
      </v-list>
    </v-navigation-drawer>
    <v-btn color="primary" @click="editInvoice">Back</v-btn>
    <v-card class="ma-12 pa-16">
      <div id="invoice_template">
        <v-row justify="center">
          <v-col md="4">
            <h3>From</h3>
            <label class="labels" for="Businesss Name">Business Name</label>
            <div>{{businessName}}</div>
            <label class="labels" for="Tax Number">Tax Number</label>
            <div>{{from_taxnumber}}</div>
            <label class="labels" for="Address Line 1">Address Line 1</label>
            <div>{{from_address1}}</div>
            <label class="labels" for="Address Line 2">Address Line 2</label>
            <div>{{from_address2}}</div>
            <label class="labels" for="City">City</label>
            <div>{{from_city}}</div>
            <label class="labels" for="Postcode">PostCode</label>
            <div>{{from_postcode}}</div>
          </v-col>
          <v-col md="4">
            <h3>To</h3>
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
            <h3>Details</h3>
            <label class="labels" for="Invoice Number">Invoice Number</label>
            <div>{{invoice_id}}</div>
            <label class="labels" for="Issue Date">Purchase Order</label>
            <div>{{purchase_order}}</div>
            <label class="labels" for="Issue Date">Issue Date</label>
            <div>{{invoice_date}}</div>
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
                  <th class="text-left">Discount Amount</th>
                  <th class="text-left">Tax</th>
                  <th class="text-left">Tax Amount</th>
                  <th class="text-left">Total</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in items" :key="index">
                  <td>{{ index +1 }}</td>
                  <td>{{item.description}}</td>
                  <td>{{item.qty}}</td>
                  <td>{{item.price}}</td>
                  <td>{{item.discount}}</td>
                  <td>{{item.discount_amount}}</td>
                  <td>{{item.tax}}</td>
                  <td>{{item.tax_amount}}</td>
                  <td>{{item.total}}</td>
                </tr>
                <tr>
                  <td>Discount:</td>
                  <td>{{itemsDiscountTotal}}</td>
                </tr>
                <tr>
                  <td>Tax:</td>
                  <td>{{itemsTaxTotal}}</td>
                </tr>
                <tr>
                  <td>Total:</td>
                  <td>{{itemsTotal}}</td>
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
</template>

<script>
import Datepicker from "vuejs-datepicker";
import html2pdf from "html2pdf.js";
export default {
  components: {
    Datepicker,
  },
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
          discount: "",
          tax: "",
          discount_amount: "",
          tax_amount: "",
          total: "",
        },
      ],
      discount_total: 0,
      tax_total: 0,
      total: 0,
      bank_name: "",
      bank_account: "",
      swift_code: "",
      invoice_notes: "",
      menu: false,
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
        discount: "",
        tax: "",
        discount_amount: "",
        tax_amount: "",
        total: "",
      });
    },
    removeItem(index) {
      if (index > 0) this.items.splice(index, 1);
    },
    itemTotal(index) {
      let itemDiscounted;
      let taxTotal;
      let taxDiscountTotal;
      //Item without tax and discount
      const calculatedTotal = this.items[index].qty * this.items[index].price;
      this.items[index].total = calculatedTotal;

      //Discount applied
      if (this.items[index].discount) {
        itemDiscounted =
          calculatedTotal * ((100 - this.items[index].discount) / 100);
        this.items[index].discount_amount =
          calculatedTotal * (this.items[index].discount / 100);
        this.items[index].total = itemDiscounted;
      } else if (
        this.items[index].discount === 0 ||
        this.items[index].discount === ""
      ) {
        this.items[index].discount_amount = 0;
      }
      // If tax applied.
      if (this.items[index].tax) {
        taxTotal = calculatedTotal * (this.items[index].tax / 100);
        this.items[index].tax_amount = taxTotal;
        this.items[index].total = taxTotal + calculatedTotal;
      } else if (this.items[index].tax === 0 || this.items[index].tax === "") {
        this.items[index].tax_amount = 0;
      }
      // If tax & discount applied.
      if (this.items[index].tax && this.items[index].discount) {
        taxDiscountTotal = itemDiscounted * (this.items[index].tax / 100);
        this.items[index].discount_amount =
          calculatedTotal * (this.items[index].discount / 100);
        this.items[index].tax_amount = taxDiscountTotal;
        this.items[index].total = itemDiscounted + taxDiscountTotal;
      }
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
    itemsTotal() {
      return this.items.reduce((acc, item) => acc + item.total, 0);
    },
    itemsDiscountTotal() {
      return this.items.reduce((acc, item) => acc + item.discount_amount, 0);
    },
    itemsTaxTotal() {
      return this.items.reduce((acc, item) => acc + item.tax_amount, 0);
    },
  },
};
</script>

<style>
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
  font-weight: 900;
  font-size: 2rem;
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
.item-index {
  padding-bottom: 22px;
}
.item-button {
  margin-bottom: 22px;
  margin-left: 5px;
  padding: 6rem;
}
tr:nth-child(2) {
  background: #f5eee8;
}
.border_bottom {
  border-bottom: lightgrey solid 2px;
}

td {
  padding-top: 26px;
}
#small-table {
  width: 100%;
}
#small-table td:nth-child(2) {
  width: 80%;
}
#small-table td {
  width: 20%;
}
#small-table td:nth-child(2) {
  width: 80%;
}
.pdf-icon {
  margin-right: 1rem;
}
button,
input,
select,
textarea {
  background-color: transparent;
  border-style: border solid 1px;
}
.datepicker input {
  border-bottom: grey 2px solid;
}
</style>