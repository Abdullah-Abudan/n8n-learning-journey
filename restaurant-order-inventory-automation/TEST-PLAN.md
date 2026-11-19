
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
