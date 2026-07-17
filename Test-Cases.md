## Test Cases..

#### Test case 01


| Field | Value |
| --- | --- |
| Test Case ID | TC- 001|
| Module | Payment|
| Title | Verify Successful Payment with Valid Visa Card|
| Preconditions | •	User account exists and is logged in •	Cart contains at least 1 in-stock item (e.g., 'Blue T-Shirt, M, Qty 2') •	Valid Visa card: 4111 1111 1111 1111, Exp 12/28, CVV 123 •	Shipping address on file|
|Test Data|Confirm that a logged-in user can complete checkout and receive order confirmation when using a valid Visa credit card.|
| Steps | 1.Log in with valid credentials 2.Navigate to cart — click cart icon top right 3.Click 'Proceed to Checkout' 4.Confirm saved address or enter: Suraram, Hyderabad 500055 5.On Payment page, select 'Credit Card'; enter card details 6.Click 'Place Order' 7.Check Order Confirmation page 8.Check email inbox for confirmation|
| Expected Result | 1.Dashboard displayed; username shown in header 2.Cart page shows correct items and subtotal 3.Checkout Step 1 (Shipping) displayed 4.Address accepted; 'Continue to Payment' button enabled 5.Card form fields accept all input; no premature errors 6.Loading spinner appears; redirect to Order Confirmation page 7.Order number displayed (e.g., ORD-20260628-1042); total matches; items listed 8.Email received within 2 minutes with order summary and tracking link |
| Priority | HIGH |
| Actual Result | All steps passed. Order ORD-20260628-1042 placed. Email received in 47 seconds.|
| Status | Pass |


#### Test Case 02

| Field | Value |
| --- | --- |
| Test Case ID | TC- 002|
| Module | Payment|
| Title | Verify Error Handling for Expired Credit Card|
| Preconditions | •	User logged in •	Cart has at least 1 item •	Expired test card: 4000 0000 0000 0069, Exp 01/22, CVV 999 |
|Test Data|Ensure the system correctly rejects an expired card and shows a clear, specific error message without losing user's entered form data.|
| Steps | 1.Complete Steps 1-4 from TC-001 (cart through shipping) 2.On Payment page, enter expired card: 4000 0000 0000 0069, Exp 01/22 3.Enter CVV 999 and billing name 'Test User' 4.Click 'Place Order' 5.Observe error message displayed 6.Inspect form fields after error 7.Verify no order was created|
| Expected Result | 1.Shipping step completed successfully 2.Fields accept input; no client-side block yet 3.CVV accepted (no hint of validity) 4.System sends to payment gateway; gateway rejects 5.CError: 'Your card has expired. Please use a different payment method.' displayed near payment section 6.Card number, CVV, name fields are retained (not cleared); only expiry date cleared or highlighted 7.No order number generated; database has no new record; no email sent |
| Priority | HIGH |
| Actual Result | ADEFECT: Error message says 'Payment failed. Try again.' — too generic. No specific mention of card expiry. DEF-001 raised.|
| Status | FAIL |


#### Test Case 03

| Field | Value |
| --- | --- |
| Test Case ID | TC- 003|
| Module | Checkout|
| Title | Apply Valid Discount Coupon and Verify Price Recalculation|
| Preconditions | •	Active coupon 'SAVE20' = 20% off orders above Rs. 500 •	Cart total = Rs. 800 (2 x items) •	User logged in|
|Test Data|Validate that a valid promotional coupon reduces the order subtotal correctly, is applied before tax, and reflects accurately across all summary views.|
| Steps | 1.Navigate to cart with Rs. 800 worth of items 2.In checkout, find 'Coupon Code' field and enter 'SAVE20' 3.Click 'Apply Coupon' 4.Observe order summary panel 5.Verify tax calculation is on discounted amount 6.Proceed to payment and place order 7.Try entering same coupon in a second session|
| Expected Result | 1.Cart shows Subtotal: Rs. 800 2.Field accepts text; 'Apply' button visible 3.System validates coupon; success message 'Coupon applied! You save Rs. 160' 4.Subtotal: Rs. 800  Discount (20%): -Rs. 160  Subtotal after discount: Rs. 640< 5.GST 18% applied on Rs. 640 = Rs. 115.20; Grand Total = Rs. 755.20 6.Order total Rs. 755.20 charged; coupon code shown in confirmation 7.Coupon is single-use per user — system rejects with 'Coupon already used'|
| Priority | MEDIUM |
| Actual Result | All steps passed. Discount calculated correctly. Tax applied on post-discount amount. Single-use restriction enforced.|
| Status | PASS |

#### Test Case 04


| Field | Value |
| --- | --- |
| Test Case ID | TC- 004|
| Module | Shipping|
| Title | Validate Form Submission Blocked with Incomplete Shipping Address|
| Preconditions | •	User logged in •	Cart has at least 1 item •	No saved address on account|
|Test Data|Confirm that client-side and server-side validation prevents checkout from proceeding when mandatory shipping fields are left blank.|
| Steps | 1.Arrive at Shipping Address step of checkout 2.Fill only: Full Name = 'Dinesh Reddy'; leave all other fields blank 3.Click 'Continue to Payment' 4.Observe validation messages 5.Fill City and PIN code only (leave phone blank) 6.Try entering invalid PIN: 'ABCDE' 7.Fill all fields with valid data; click Continue 8.Simulate POST request with missing fields via browser dev tools|
| Expected Result | 1.Empty form with all mandatory fields marked with red asterisk (*) 2.Only name field filled 3.Button click triggers validation; page does NOT navigate away 4.Inline errors appear: 'Address is required', 'City is required', 'PIN Code is required', 'Phone is required' 5.Phone field still shows error; others cleared 6.Error: 'Please enter a valid 6-digit PIN code' 7.Validation passes; user proceeds to Payment step 8.Server returns 400 Bad Request with field-level error JSON|
| Priority | HIGH |
| Actual Result | Client validation passed. Server-side validation confirmed via Postman. All mandatory fields enforced.|
| Status | Pass |


#### Test Case 05


| Field | Value |
| --- | --- |
| Test Case ID | TC- 005|
| Module | Checkout|
| Title | Guest Checkout — Full Flow Without Account Registration|
| Preconditions | •	Browser in incognito/private mode (no saved session) •	Valid email address ready •	Test item: 'Black Notebook, Qty 1, Rs. 299'|
|Test Data|Verify that a non-registered user can browse, add to cart, and complete checkout as a guest using only their email address, receiving confirmation without account creation.|
| Steps | 1.Open site in incognito; browse to product page; add item to cart 2.Click cart icon; click 'Proceed to Checkout'  3.Click 'Continue as Guest'; enter email: testguest@gmail.com 4.Enter full shipping address 5.On Payment page, enter valid test card details 6.Click 'Place Order' 7.Check email testguest@gmail.com for confirmation 8.Attempt to log in with that email (no password set)|
| Expected Result | 1.Item added to cart; cart icon shows count 1 2.Login page OR guest checkout option presented 3.Guest checkout form opened; no password required 4.Address accepted; standard shipping rate applied 5.Payment form accepts input 6.Order placed; confirmation page shown with order number 7.Confirmation email received with order details and guest account creation CTA 8.'No account found. Create one?' message — account NOT auto-created|
| Priority | MEDIUM |
| Actual Result | Guest checkout completed successfully. Confirmation email received in 38 seconds. No account auto-created.|
| Status | Pass |
