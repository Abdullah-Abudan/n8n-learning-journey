
## TC-01 — Valid Order Submission

**Workflow:** 01 - Order Intake  
**Status:** Passed

**Objective:**  
Verify that a valid customer order is received, assigned a unique Order ID, saved in Google Sheets, and reported to the manager through Telegram.

**Test Data:**
- Customer Name: Test Customer
- Phone Number: 0590000000
- Order Items: Valid product from Recipes
- Notes: TC-01 Test

**Expected Results:**
1. A unique Order ID is generated.
2. The order status is set to `Pending`.
3. The order is saved as a new row in the `Orders` sheet.
4. A Telegram notification is sent to the manager.
5. Inventory quantities remain unchanged.

**Actual Results:**
- A new Order ID was generated successfully.
- The order was saved with `Pending` status.
- The order appeared in Google Sheets.
- The Telegram notification was received.
- No inventory deduction occurred.

**Result:** Passed

**Evidence:**
- `screenshots/testing/TC-01-order-created.png`
- `screenshots/testing/TC-01-telegram-notification.png`


## TC-02 — Missing Required Fields

**Workflow:** 01 - Order Intake  
**Status:** Passed

**Objective:** Verify that the order form prevents submission when required fields are missing.

### TC-02A — Missing Customer Name
- **Test:** Leave Customer Name empty.
- **Expected:** Form submission is blocked.
- **Actual:** The form prevented submission.
- **Result:** Passed
- **Evidence:** `screenshots/testing/TC-02A-missing-customer-name.png`

### TC-02B — Missing Phone Number
- **Test:** Leave Phone Number empty.
- **Expected:** Form submission is blocked.
- **Actual:** The form prevented submission.
- **Result:** Passed
- **Evidence:** `screenshots/testing/TC-02B-missing-phone-number.png`


## TC-03 — Multiple Products in One Order

**Workflow:** 01 - Order Intake  
**Status:** Passed

**Objective:** Verify that a single order can contain multiple products with different quantities.

**Test Data:**
- Burger x 2
- Burger with cheese x 1

**Expected Results:**
1. One unique Order ID is generated.
2. Both products and their quantities are saved in the same order.
3. Order status is set to `Pending`.
4. Telegram notification includes both products and quantities.
5. Inventory remains unchanged.

**Actual Results:**
All expected results were verified successfully.

**Result:** Passed

**Evidence:**
- `screenshots/testing/TC-03-multiple-products-order.png`
- `screenshots/testing/TC-03-multiple-products-telegram.png`


## TC-04 — Successful Order Completion

**Workflows:** 02 - Order Status Management, 03 - Inventory Management  
**Related Test Case:** TC-03  
**Status:** Passed (pending verification of stock records)

**Objective:**
Verify that completing a pending order triggers inventory deduction, records stock movements, and updates the order status.

**Test Data:**
- Order: The order created in TC-03
- Burger x 2
- Burger with cheese x 1

**Test Steps:**
1. Submit the `done ORDER-ID` command through Telegram.
2. Verify the order completion response.
3. Check the order status in Google Sheets.
4. Verify the inventory quantities after deduction.
5. Verify the corresponding stock movement records.

**Expected Results:**
1. The order is completed successfully.
2. The order status changes from `Pending` to `Done`.
3. Required ingredient quantities are deducted according to the product recipes.
4. Stock movements are recorded against the same Order ID.
5. No duplicate deduction occurs.

**Actual Results:**
- The completion command was processed successfully.
- The order completion flow returned a successful result.

**Evidence:**
- `screenshots/testing/TC-04-telegram-completion.png`
- `screenshots/testing/TC-04-order-status-done.png`
- `screenshots/testing/TC-04-inventory-after-deduction.png`
- `screenshots/testing/TC-04-stock-movements.png`


### TC-04 — Successful Order Completion

**Expected Result:**
- Order status changes from Pending to Done.
- Required ingredients are deducted from inventory.
- Stock movements are recorded for the order.
- A Telegram completion confirmation is sent to the manager.

**Actual Result:**
- Order status was successfully updated from Pending to Done.
- Required ingredients were deducted from inventory in the correct quantities.
- Stock movements were successfully recorded for the order.
- Telegram completion confirmation was successfully sent to the manager.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-04-order-status-done.png`
- `screenshots/testing/TC-04-telegram-completion.png`
- `screenshots/testing/TC-04-inventory-after-deduction.png`
- `screenshots/testing/TC-04-stock-movements.png`


### TC-05 — Insufficient Stock

**Test Data:**
- Product: Burger
- Quantity: 200

**Expected Result:**
- The order remains Pending.
- The system detects insufficient inventory.
- No inventory quantities are deducted.
- No stock movements are recorded for the order.

**Actual Result:**
- The order remained Pending after the completion attempt.
- The system correctly detected insufficient inventory.
- Inventory quantities remained unchanged.
- No stock movements were recorded for the order.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-05-order-created.png`
- `screenshots/testing/TC-05-insufficient-stock-response.png`
- `screenshots/testing/TC-05-inventory-unchanged.png`
- `screenshots/testing/TC-05-stock-movements-unchanged.png`


### TC-06 — Missing Inventory Ingredient

**Test Data:**
- Product: Burger
- Quantity: 1
- Missing Ingredient: Test Ingredient
- Recipe was temporarily updated to include the missing ingredient.

**Expected Result:**
- The system detects the missing inventory ingredient.
- The order remains Pending.
- No inventory quantities are deducted.
- No stock movements are recorded for the order.

**Actual Result:**
- The system correctly detected the missing ingredient.
- The order remained Pending.
- Inventory quantities remained unchanged.
- No stock movements were recorded for the order.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-06-order-created.png`
- `screenshots/testing/TC-06-missing-ingredient-response.png`
- `screenshots/testing/TC-06-inventory-unchanged.png`


### TC-07 — Cancel Pending Order

**Test Data:**
- Product: Burger
- Quantity: 1
- Initial Order Status: Pending

**Expected Result:**
- The order status changes from Pending to Cancelled.
- A Telegram cancellation confirmation is sent to the manager.
- Inventory quantities remain unchanged.
- No stock movements are recorded for the cancelled order.

**Actual Result:**
- The order status was successfully updated from Pending to Cancelled.
- Telegram cancellation confirmation was successfully sent to the manager.
- Inventory quantities remained unchanged.
- No stock movements were recorded for the cancelled order.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-07-order-cancelled.png`
- `screenshots/testing/TC-07-telegram-cancellation.png`
- `screenshots/testing/TC-07-inventory-unchanged.png`


### TC-08 — Cancel Non-Pending Order

**Test Data:**
- Order Status: Cancelled
- Command: cancel

**Expected Result:**
- The system rejects the cancellation request.
- The order status remains unchanged.
- No inventory changes occur.
- No stock movements are recorded.

**Actual Result:**
- The system rejected the cancellation request.
- Telegram returned: "Order Cannot Be Cancelled".
- The current status was correctly identified as Cancelled.
- The system confirmed that only Pending orders can be cancelled.
- No changes were made to the order or inventory.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-08-telegram-cancellation-rejected.png`
- `screenshots/testing/TC-08-order-status-unchanged.png`



### TC-09 — Complete Non-Pending Order

**Test Data:**
- Order ID: Existing TC-07 order
- Initial Order Status: Cancelled
- Command: done

**Expected Result:**
- The system rejects the completion request.
- The order status remains Cancelled.
- No inventory deduction is performed.
- No new stock movements are recorded.

**Actual Result:**
Pending verification.

**Status:** Not Tested

**Evidence:**
- `screenshots/testing/TC-09-telegram-completion-rejected.png`
- `screenshots/testing/TC-09-order-status-unchanged.png`

### TC-10 — Order Not Found

**Test Data:**
- Order ID: ORD-99999999
- Command: done

**Expected Result:**
- The system detects that the order does not exist.
- A Telegram error message is returned.
- No order or inventory data is modified.

**Actual Result:**
- The system correctly identified that the order does not exist.
- Telegram returned an Order Not Found response.
- No data was modified.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-10-order-not-found.png`


### TC-11 — Invalid Telegram Command

**Test Data:**
- Command: hello

**Expected Result:**
- The system rejects the invalid Telegram command.
- A message explaining the valid command format is returned.
- No order or inventory data is modified.

**Actual Result:**
- The system correctly rejected the invalid Telegram command.
- Telegram returned a response indicating that the command format is invalid.
- No order or inventory data was modified.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-11-invalid-telegram-command.png`


### TC-12 — Unauthorized Manager

**Test Data:**
- Command: done
- Order Status: Pending
- Sender: Unauthorized Telegram User

**Expected Result:**
- The system rejects commands from unauthorized users.
- The order status remains Pending.
- No inventory quantities are deducted.
- No stock movements are recorded.

**Actual Result:**
- The system correctly rejected the unauthorized user's command.
- The order remained Pending.
- No inventory changes were performed.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-12-unauthorized-manager.jpg`

