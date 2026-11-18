
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
