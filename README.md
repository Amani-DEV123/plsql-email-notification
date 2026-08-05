# Pending Sales Orders Email Notification

A PL/SQL procedure was developed to automatically send email notifications to sales representatives for pending sales orders.

The procedure retrieves sales orders with a status of **'F'** that have remained pending for more than one day using the following condition:

```sql
TRUNC(ORDER_DATE) <= TRUNC(SYSDATE) - 1
```

The system groups pending orders by **sales representative (EMP_CODE)**. Each sales representative receives a personalized HTML email containing only the customers and orders assigned to them.

The email includes the following information:

* Order ID
* Order Date
* Customer Name
* Customer Mobile
* Total Amount

## Cursor Implementation

Two cursors were used to organize the email generation process efficiently:

* **Cursor C1:** Retrieves the list of unique sales representatives who have pending sales orders. This ensures that each representative is processed only once.

* **Cursor C2:** Retrieves all pending sales orders assigned to the current sales representative from Cursor C1.

Using two cursors allows the system to send **one email per sales representative** containing a complete summary table of all assigned customers and pending orders, instead of sending multiple emails for each individual order.

This approach improves order tracking by helping sales representatives quickly identify pending orders that require follow-up actions and ensures that each representative receives only the information related to their assigned customers.
