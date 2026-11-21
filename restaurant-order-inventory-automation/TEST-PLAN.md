
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
- The system rejected the completion request for the Cancelled order.
- The order status remained Cancelled.
- No inventory deduction was performed.
- No new stock movements were recorded.

**Status:** Passed

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

### TC-13 — Recovery with Matching Movements

**Test Data:**
- Order: Previously processed order
- Existing Stock Movements: Matching recipe quantities
- Command: done

**Expected Result:**
- The system validates existing stock movements.
- Recovery succeeds without duplicate inventory deduction.
- No additional stock movements are recorded.

**Actual Result:**
- The system successfully validated the existing stock movements.
- Recovery completed successfully.
- No duplicate inventory deduction occurred.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-13-recovery-matching-movements.png`


### TC-14 — Recovery with Mismatched Movements

**Expected Result:**
- The system detects mismatched stock movements.
- Recovery is rejected.
- No additional inventory deduction occurs.

**Actual Result:**
- The system detected mismatched existing stock movements.
- Recovery validation failed as expected.
- The system returned a Manual Review response.
- No additional inventory deduction was performed.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-14-recovery-mismatched-movements.png`
- `screenshots/testing/TC-14-recovery-mismatched-movements-sheet.png`

### TC-15 — Recovery with Incomplete Movements

**Test Data:**
- Product: Burger
- Order Quantity: 1
- Existing Stock Movement: Bread — 1 OUT
- Missing Movement: Beef Patty

**Expected Result:**
- The system detects incomplete existing stock movements.
- Recovery is rejected.
- No additional inventory deduction occurs.
- The order remains Pending.
- A Manual Review notification is returned.

**Actual Result:**
- The system detected existing incomplete stock movements.
- Telegram returned an Order Requires Manual Review notification.
- No additional inventory was deducted.
- The order remained Pending.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-15-recovery-incomplete-movements.png`
- `screenshots/testing/TC-15-recovery-incomplete-movements-sheet.png`



### TC-16 — Zero or Negative Product Quantity

**Test Data:**
- Product: Burger
- Quantities Tested: 0 and -1

**Expected Result:**
- The system should reject zero and negative quantities.
- Invalid orders should not be completed.
- Inventory must remain unchanged.
- No stock movements should be recorded.

**Actual Result:**
- Workflow 01 accepted both quantities and created orders.
- Workflow 03 rejected quantity 0 with: `Invalid product or quantity`.
- Workflow 03 rejected quantity -1 with: `Invalid item format`.
- Neither order was completed.

**Status:** Passed

**Note:**
Input validation is handled during inventory processing rather than at order submission.

**Evidence:**
- `screenshots/testing/TC-16-zero-quantity-rejected.png`
- `screenshots/testing/TC-16-negative-quantity-rejected.png`

### TC-17 — Missing Product Recipe

**Test Data:**
- Product: Test Product
- Quantity: 2
- Order ID: ORD-2026-11-21-583

**Expected Result:**
- The system should detect that the product has no recipe.
- The order should not be completed.
- Inventory quantities should remain unchanged.
- No stock movements should be recorded.

**Actual Result:**
- The order was successfully created with PENDING status.
- Workflow 03 returned: `Recipe not found for: Test Product`.
- The order remained PENDING.
- Inventory quantities remained unchanged.
- No stock movements were recorded.

**Status:** Passed

**Evidence:**
- `screenshots/testing/TC-17-missing-product-recipe.png`