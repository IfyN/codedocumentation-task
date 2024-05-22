#TASK

Sellers on the Paddle platform often run promotions around Black Friday and Cyber Monday,
offering discounted access to their subscriptions or on one-time products like ebooks.
We’d like for you to write a tutorial that walks us through how you’d set up a discount for a Black
Friday sale in Paddle Billing.
Many sellers are indie hackers who are new to software, so they’ve never run promotions
before. We’re trying to build a reputation in the industry as the most helpful brand in SaaS, so
it’d be great to talk about best practices for offering discounts generally as well as how they
work and how to set them up using Paddle.
Remember tutorials assume little or no knowledge, and walk the user through doing something
from start to finish — they include everything a user needs to know to complete a task.
To get started, we recommend checking out:

● Our existing how-to on creating a discount:
https://developer.paddle.com/build/products/offer-discounts-promotions-coupons
● Our guide on how-to prefill a discount at checkout:
https://developer.paddle.com/build/checkout/prefill-checkout-properties
● The Paddle API for discounts:
https://developer.paddle.com/api-reference/discounts/overview
● The Paddle.com blog, which contains a bunch of articles about pricing and discount
strategy
https://www.paddle.com/blog


#Solution


#Run promotions and discounts for Black Friday and Cyber Monday

Black Friday and Cyber Monday discounts offer special deals during promotions to attract new customers and boost sales. They're limited-time discounts, typically valid for a short period, and can apply to specific products or all items in your catalog.

#### WEB

##### **Create a New Discount**

**Discount type:**

* **Percentage:** Fill out the percentage off details.
* **Amount:** Fill out the amount details and select the currency.
* **Amount per unit:** Fill out the amount details and select the currency.
&nbsp;
Enter a descriptive name for the discount for example, 'Black Friday Sale'

##### **Recurring Black Friday Discounts**

If you want the black Friday discount to apply to future black Friday and Cyber Monday promotions.

- Until further notice: the discount: the discount should recur forever
A number to set a number of billing periods..
- For a custom number of billing periods: the discount should recur for a set number of billing periods.

Check the **Set an expiration date for the discount** box, then enter a date and time.

Check the **Limit the number of times this discount** box.

####API 

Send a POST request to the `/discounts` endpoint, setting recurs to true and `maximum_recurring_intervals` to either:

- `null` to set a discount to recur forever.
- A number to set a number of billing periods.

#####Request

```{
  "recur": true,
  "maximum_recurring_intervals": 3
  }
```
#####Response

##### **Create a Discount Code**

Set the **Checkout discount code** toggle on.
Set a discount code or select the **Generate random code** option.

##### **Limit Black Friday Discount to Certain Products**

Set the **Limit discount to selected product** toggle on, then use the products and prices dropdowns to choose which products and prices this discount applies to.

Select **+Products** to add more product options.

####API
`https://api.paddle.com/discounts`

#####Request
```
{
  "description": "Black Friday Sale",
  "type": "percentage",
  "amount": "10",
  "enabled_for_checkout": true,
  "recur": true,
  "maximum_recurring_intervals": 3,
  "expires_at": "2024-12-03T00:00:00Z"
  "code": "10OFF"
  "restrict_to": [
    "pri_01gsz8z1q1n00f12qt82y31smh",
    "pri_01gsz8s48pyr4mbhvv2xfggesg"
  ]
}
```
#####Response

```
{
  "data": {
    "id": "dsc_01hv6scyf7qdnzcdq01t2y8dx4",
    "status": "active",
    "description": "Seasonal sale",
    "enabled_for_checkout": true,
    "code": "SEWRGPB9WY",
    "type": "percentage",
    "amount": "10",
    "currency_code": null,
    "recur": true,
    "maximum_recurring_intervals": 3,
    "usage_limit": null,
    "restrict_to": null,
    "expires_at": "2024-12-03T00:00:00Z",
    "times_used": 0,
    "custom_data": null,
    "import_meta": null,
    "created_at": "2024-04-11T14:36:14.695Z",
    "updated_at": "2024-04-11T14:36:14.695Z"
  },
  "meta": {
    "request_id": "1681f87f-9c36-4557-a1da-bbb622afa0cc"
  }
}
```
