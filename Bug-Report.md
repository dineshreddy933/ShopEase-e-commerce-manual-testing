## Bug-Report 

#### Defect report 001

| Field | Value |
| --- | --- |
| Bug ID | BUG- 001|
| Title | Generic Error Message Displayed for Expired Credit Card|
| Module | Payment |
| Environment | Staging | Chrome 126 | macos26.5 | ShopEase v2.4.1|
| Preconditions | When a user enters an expired credit card and clicks 'Place Order', the error message displayed is 'Payment failed. Please try again.' This is too generic and does not inform the user WHY the payment failed.|
| Steps to Reproduce | 1.	Log in with valid credentials 2.	Add any in-stock item to cart 3.	Proceed to checkout — complete shipping step 4.	On Payment page, enter: Card No: 4000 0000 0000 0069 | Exp: 01/22 | CVV: 999 5.	Click 'Place Order' 6.	Observe the error message displayed on screen|
| Actual Result | Error shown: 'Payment failed. Please try again.' — no mention of card expiry|
| Expected Result |Error should read: 'Your card has expired. Please check the expiry date or use a different card.' — specific and actionable|
| Severity | Medium |
| Priority | High |
| Evidence | screenshot|
| Status | OPEN |



<img width="1470" height="956" alt="Screenshot 2026-06-28 at 11 53 57 PM" src="https://github.com/user-attachments/assets/6778e6d3-9f57-490e-9150-40ed74a0b15d" />


#### Defect report 002

| Field | Value |
| --- | --- |
| Bug ID | BUG- 002|
| Title |Session Expiry During Checkout Clears Cart Items|
| Module | Checkout|
| Environment |Staging | Chrome 126 | macOS26.5 | ShopEase v2.4.1|
| Preconditions | When a logged-in user's session expires while they are on the checkout page, upon re-login they are redirected to an empty cart. All previously added items are lost, and the user must start shopping again from scratch.|
| Steps to Reproduce | 1.Log in with valid user credentials. 2.	Add 3+ items to the cart (note the items and quantities) 3.	Navigate to checkout and reach the Shipping Address step 4.	Leave the browser idle for 35 minutes (session timeout = 30 min) 5.	Click any button on the checkout page (e.g., 'Continue to Payment') 6.	Observe the session expired prompt or redirect7.	Log in again with valid credentials 8.	Observe the cart state after login|
| Actual Result | After re-login, cart is completely empty. All 3 items that were present before session expiry are gone. User must search and add items again.|
| Expected Result | Cart items should persist across session expiry for logged-in users. Items should be stored in the database against the user's account, not only in the session/localStorage. After re-login, cart should be fully restored.|
| Severity |  High |
| Priority | High |
| Evidence | screenshot |
| Status | OPEN |
 
<img width="1470" height="956" alt="Screenshot 2026-06-28 at 11 56 51 PM" src="https://github.com/user-attachments/assets/418291d7-c64b-4714-9b51-a0616a911e5a" />
