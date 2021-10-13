```
UserManagement


1. Customer, Purchase Order, Invoice
2. Items with some Category. Computer Hardware Storage-->Pen drive,HDD,...Cpu
3. Customer Place order
4. PO -->Against Customer order one PO will be created
5. PO must be Signed by Customer 
6. If PO is not signed by Customer in 5 Days then PO will be cancelled and Order must be cancelled with reason PO not signed.
7. If PO is signed with in 5 days then you need to create an Invoice with unique InvoiceId and dispatch to customer.
8. Payment for the invoice is due in 30 days
9. Return form where Customer can return the item but with in 10 days. Item should be updated in the stock and Return item amount is to be adusted in customer's balance.


Reports

 Current Balance , Defaulters list ,Invoice wise list
Issue list

Console App :- File item list, Upload that file in the database

Notification Service:

If invoice payment is due more than 30 days then notification should sent to the customer
PO if it is not signed with in 2 days then send daily reminder till day 5

API GATEWAY
EUREKA WEBSERVER


UserManagement --Admin , Regular Shubham
``
