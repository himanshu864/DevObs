#nodejs

Designing data models for NodeJS applications using Mongoose.

Suppose you're creating an e-commerce website. And designing it's data models of orders. Every order belongs to a customer, has a price tag, has delivery status and contains a List of Order Items. But how do you define Array of Items in a data model?

*By creating a separate schema*. Define type as : [orderItemSchema]

```javascript
import mongoose from 'mongoose';

const orderItemSchema = new mongoose.Schema({
	productId: {
		type: mongoose.Schema.Types.ObjectId,
		ref = "Product",
	},
	quantity: {
		type: Number,
		required: true,
	}
})

const orderSchema = new mongoose.Schema({
	customer: { // referencing User data model
		type: mongoose.Schema.Types.ObjectId,
		ref = "User", // compulsory ref
	},
	orderPrice: {
		type: Number,
		required: true,
	},
	status: { // To define fixed values to choose from
		type: String,
		enum: ["PENDING", "CANCELLED", "DELIVERED"],
		default: "PENDING"
	},
	orderItems: {
		type: [orderItemSchema]
	}
}, {timestamps: true})

export const Order = mongoose.model("Order", orderSchema);
```

Or can simple define schema inside []
```javascript
const orderSchema = new mongoose.Schema({
	// ...
	orderItems: {
		type: [{
				productId: {/*...*/},
				quantity: {/*...*/},
			}
		]
	}
}, {timestamps: true})
```

