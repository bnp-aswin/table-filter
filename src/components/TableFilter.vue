<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col">
                <form class="row g-3">
                    <div class="col-auto">
                        <label for="order-id">Order Id</label>
                        <input 
                            @blur="resultData()"
                            v-model="givenOrderId"
                            type="number"
                            class="form-control"
                            id="order-id"
                            placeholder="Order Id"
                        />
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Tracking No</label>
                        <input
                            @blur="resultData()"
                            v-model="givenTrackNo"
                            type="number"
                            class="form-control"
                            id="tracking-no"
                            placeholder="Tracking No"
                        />
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Customer Name</label>
                        <input
                            @blur="resultData()"
                            v-model="givenCustomerName"
                            type="text"
                            class="form-control"
                            id="customer-name"
                            placeholder="Customer Name"
                        />
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Reference No</label>
                        <input
                            @blur="resultData()"
                            v-model="givenReferenceNo"
                            type="number"
                            class="form-control"
                            id="reference-no"
                            placeholder="Reference No"
                        />
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Order Status</label>
                        <select
                            @change="resultData()"
                            v-model="selectedOrderStatus"
                            id="order-status"
                            class="form-control"
                        >
                            <option value="" disabled selected hidden
                                >Select Status</option
                            >
                            <option
                                v-for="(status, index) in orderStatusOptions"
                                :value="status"
                                :key="index"
                            >
                                {{ status }}
                            </option>
                        </select>
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Couriers Options</label>
                        <select
                            @change="resultData()"
                            v-model="selectedCourierPartner"
                            id="couriers-options"
                            class="form-control"
                        >
                            <option value="" disabled selected hidden
                                >Select Couriers</option
                            >
                            <option
                                v-for="(courier, index) in couriersOptions"
                                :value="courier"
                                :key="index"
                            >
                                {{ courier }}
                            </option>
                        </select>
                    </div>
                    <div class="col-auto">
                        <label for="order-id">Shipping Mode</label>
                        <select
                            @change="resultData()"
                            v-model="selectedShippingMode"
                            id="shipping-mode"
                            class="form-control"
                        >
                            <option value="" disabled selected hidden
                                >Select Mode</option
                            >
                            <option
                                v-for="(mode, index) in shippingModeOptions"
                                :value="mode"
                                :key="index"
                            >
                                {{ mode }}
                            </option>
                        </select>
                    </div>
                    <input @click="resultData()" type="button" value="Search" />
                    <!-- <div class="col-auto">
                    <button type="submit" class="btn btn-primary mb-3">Find Order</button>
                </div> -->
                </form>
            </div>
        </div>
        <div class="row mt-5">
            <table class="table table-success table-striped">
                <thead>
                    <tr>
                        <th>Placed On</th>
                        <th>Order Id</th>
                        <th>Customer Name</th>
                        <th>Shipping Mode</th>
                        <th>Reference</th>
                        <th>Courier</th>
                        <th>Tracking Id</th>
                        <th>Status</th>
                        <th>Actions</th>
                        <th>Returned On</th>
                        <th>Days Left</th>
                        <th>Re-Ship</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(order, index) in searchResult" :key="index">
                        <td>{{ order.placedOn }}</td>
                        <td>{{ order.orderId }}</td>
                        <td>{{ order.customerName }}</td>
                        <td>{{ order.shippingMode }}</td>
                        <td>{{ order.reference }}</td>
                        <td>{{ order.courier }}</td>
                        <td>{{ order.trackingId }}</td>
                        <td>{{ order.status }}</td>
                        <td>{{ order.actions }}</td>
                        <td>{{ order.returnedOn }}</td>
                        <td>{{ order.daysLeft }}</td>
                        <td>{{ order.reShip }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    props: {},
    data() {
        return {
            orders: [
                {
                    placedOn: "2021-05-20",
                    orderId: 1123,
                    customerName: "Customer 1",
                    shippingMode: "COD",
                    reference: 20,
                    courier: "FedEx Surface",
                    trackingId: 12132,
                    status: "Delivered",
                    actions: "action 1",
                    returnedOn: "2017-06-14",
                    daysLeft: 10,
                    reShip: "re-ship-1",
                },
                {
                    placedOn: "2021-03-25",
                    orderId: 1126,
                    customerName: "Customer 2",
                    shippingMode: "International",
                    reference: 55,
                    courier: "India Post",
                    trackingId: 12732,
                    status: "Processing",
                    actions: "action 3",
                    returnedOn: "2017-04-11",
                    daysLeft: 19,
                    reShip: "re-ship-5",
                },
                {
                    placedOn: "2021-02-28",
                    orderId: 1128,
                    customerName: "Customer 3",
                    shippingMode: "Standard Shipping",
                    reference: 88,
                    courier: "Xpressbees",
                    trackingId: 12832,
                    status: "Received",
                    actions: "action 6",
                    returnedOn: "2017-12-10",
                    daysLeft: 10,
                    reShip: "re-ship-3",
                },
                {
                    placedOn: "2021-07-10",
                    orderId: 1120,
                    customerName: "Customer 4",
                    shippingMode: "COD",
                    reference: 19,
                    courier: "Ecom Express",
                    trackingId: 12232,
                    status: "Undelivered",
                    actions: "action 9",
                    returnedOn: "2017-10-24",
                    daysLeft: 50,
                    reShip: "re-ship-7",
                },
                {
                    placedOn: "2021-09-19",
                    orderId: 1129,
                    customerName: "Customer 5",
                    shippingMode: "International",
                    reference: 96,
                    courier: "Delhivery",
                    trackingId: 12532,
                    status: "Undelivered",
                    actions: "action 2",
                    returnedOn: "2017-02-14",
                    daysLeft: 90,
                    reShip: "re-ship-0",
                },
                {
                    placedOn: "2021-02-13",
                    orderId: 1124,
                    customerName: "Customer 6",
                    shippingMode: "Standard Shipping",
                    reference: 43,
                    courier: "Ecom Express",
                    trackingId: 12932,
                    status: "Delivered",
                    actions: "action 8",
                    returnedOn: "2017-01-19",
                    daysLeft: 30,
                    reShip: "re-ship-1",
                },
                {
                    placedOn: "2021-04-04",
                    orderId: 1127,
                    customerName: "Customer 7",
                    shippingMode: "COD",
                    reference: 29,
                    courier: "Blue Dart",
                    trackingId: 12632,
                    status: "Received",
                    actions: "action 7",
                    returnedOn: "2017-12-10",
                    daysLeft: 70,
                    reShip: "re-ship-2",
                },
            ],
            orderStatusOptions: [
                "All",
                "Received",
                "Out of Stock",
                "On Hold - Out of Stock",
                "Processing",
                "QC Passed",
                "Ready to Dispatch",
                "Shipped",
                "Shipment Cancelled",
                "In Transit",
                "Out for Delivery",
                "Delivered",
                "Undelivered",
                "RTO Initiated",
                "Added to Returns",
                "Refunded",
                "Partially Refunded",
                "Cancelled",
                "Moved To Inventory",
                "Additional Info Required",
                "Disposal Initiated",
                "Disposed",
            ],
            couriersOptions: [
                "All",
                "India Post",
                "Aramex(I)",
                "Delhivery",
                "Ecom Express",
                "Xpressbees",
                "Blue Dart",
                "FedEx Surface",
                "DHL Packet International",
                "DHL Packet Plus International",
                "DHL Parcel International Direct",
                "Ekart",
                "Delhivery Surface Standard",
                "Xpressbees Surface",
                "Amazon Easy Ship (Self)",
                "Snapdeal (Self)",
                "Flipkart (Self)",
                "FedEx (Self)",
                "Delhivery (Self)",
                "Ekart (Self)",
                "Ecom (Self)",
                "Xpressbees (Self)",
                "Aramex (Self)",
                "Blue Dart (Self)",
                "DTDC (Self)",
                "DHL (Self)",
                "Vulcan (Self)",
            ],
            shippingModeOptions: [
                "All",
                "COD",
                "Standard Shipping",
                "International",
            ],
            getOrderId: "",
            getTrackingNo: "",
            getName: "",
            getReferenceNo: "",
            getOrderStatus: "",
            getCourierOption: "",
            getShippingMode: "",
            // resultData:[],
            givenOrderId: "",
            givenTrackNo: "",
            givenCustomerName: "",
            givenReferenceNo: "",
            selectedOrderStatus: "",
            selectedCourierPartner: "",
            selectedShippingMode: "",
            searchResult: [],
        };
    },
    methods: {
        // filterByOrderId(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.orderId===this.getOrderId;
        //   },this)
        // },
        // filterByTrackingNo(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.trackingId===this.getTrackingNo;
        //   },this)
        // },
        // filterByName(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.customerName===this.getName;
        //   },this)
        // },
        // filterByReferenceNo(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.reference===this.getReferenceNo;
        //   },this)
        // },
        // filterByOrderStatus(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.status===this.getOrderStatus;
        //   },this)
        // },
        // filterByCourier(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.courier===this.getCourierOption;
        //   },this)
        // },
        // filterByShipping(){
        //   this.resultData= this.orders.filter(function(el){
        //    return el.shippingMode===this.getShippingMode;
        //   },this)
        // },
        resultData() {
            let filterOrderId = this.givenOrderId,
            filterTrackNo=this.givenTrackNo,
            filterCustomerName=this.givenCustomerName,
            filterReferenceNo=this.givenReferenceNo,
            filterOrderStatus=this.selectedOrderStatus,
            filterCourierPartner=this.selectedCourierPartner,
            filterShippingMode=this.selectedShippingMode;
            this.searchResult = this.orders.filter(function(item) {
                let filtered;
                if (filterOrderId != '') {
                    filtered = item.orderId == filterOrderId;
                }
                if (filterTrackNo != '') {
                    filtered = item.trackingId == filterTrackNo;
                }
                if (filterCustomerName != '') {
                    filtered = item.customerName == filterCustomerName;
                }
                if (filterReferenceNo != '') {
                    filtered = item.reference == filterReferenceNo;
                }
                if (filterOrderStatus != '') {
                    filtered = item.status == filterOrderStatus;
                }
                if (filterCourierPartner != '') {
                    filtered = item.courier == filterCourierPartner;
                }
                if (filterShippingMode != '') {
                    filtered = item.shippingMode == filterShippingMode;
                }
                return filtered;
            });
        },
    },
    computed: {},
    mounted() {
      this.resultData();
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
    padding: 15px 20px;
}
</style>
