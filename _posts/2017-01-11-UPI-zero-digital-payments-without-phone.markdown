---
author: admin
comments: true
layout: post
title: UPI Zero - Digital Payments without Phone 
---


### What is UPI-card ?
 UPI-card is a plain plastic card with a grid of numbers printed on it. UPI-card can be enhanced with a magnetic stripe or a smart chip inside.
The grid of numbers is random and unique to every single card. This is not a new invention. ICICI Bank already uses it today and is compliant with RBI mandates on 2-factor authentication.

[![Card Grid](/images/2017-01-11-UPI-zero-digital-payments-without-phone/card-grid.png)](/images/2017-01-11-UPI-zero-digital-payments-without-phone/card-grid.png)


### How does UPI-card work ?

UPI-card can be used without internet or smartphone. UPI-card's authentication mechanism works on SMS - **we have eliminated the requirement of UPI to use 3g/internet/USSD.**
UPI-card works with the NPCI/UPI service provider. Instead of using a phone based OTP, the UPI-card uses random numbers from the number grid to verify the customer. Please note that a similar mechanism is already being used by ICICI for their netbanking infrastructure.  **This is a proven piece of technology that can work at scale.**
By doing this, we eliminate the need for every customer to carry a phone: The customer does **NOT** need to have even a regular phone. **Only** the shopkeeper needs to have a simple phone capable of sending SMS.
**We have brought down the requirement of UPI from a billion phones to just about hundred million.**


### Why SMS versus USSD?

Our solution is targeted towards retail purchases - where money **transfers happen very frequently and very quickly and typically a lot of people are waiting in line**. We believe the 3 step SMS mechanism is far superior to USSD because it allows the shopkeeper to service multiple people in parallel without forgetting who he is working  with or without being forced to go through an entire payment process before addressing the other customer.
In addition, the SMS works as a ledger that can be used by the shopkeepers. Remember that frequently shopkeepers use their assistants to do all the work - this will be a ledger of everything that happened that day (including failed transactions).

### How is UPI-card distributed/issued ?

We are borrowing ideas from the highly successful **m-Pesa project in Kenya**. UPI-card will be distributed by any kirana stores. People will not have to go to banks to get one. **We are eliminating the bottleneck of  current banking infrastructure.**
Every kirana store will have a special e-wallet issued by respective bank. This special wallet will be used to load money into customer wallet. This is very similar to how mobile recharge already works.
**Any bank can issue their own UPI-card. Since it uses the NPCI/UPI infrastructure, we can guarantee compatibility.**
In the back end, a UPI-card is actually a real bank account + UPI id which is created in one-shot. It's a win-win for banks since their accounts+deposits go up.

### What about KYC/AML regulations?

The money is fronted by the kirana store in the first place and then gets it reimbursed by the bank. This shifts the onus of  KYC/AML responsibility to the kirana store and is highly scalable. This is the reason why m-Pesa is able to do this in a scalable way in Kenya.
This is also an opportunity by which issuing bank can control the flow of money in a particular geographical area because they already know the spend patterns in different areas. This will cut down on fraudulent transactions.
We also propose to onboard and train the kirana stores to use Aadhaar e-kyc for customers.


### How does a sample shopping process look like

`UPIZ 3456324 500 `  
- charge UPI-card# 3456324, amount=500

 
`3456324 500 1 8 23 4 6`    
- UPI-Zero gateway is asking for secret numbers in boxes 1,8,23,4,6 . Let us assume the secret numbers (as printed on the UPI-card are 88,0,9,3,4)
 

`UPIZ 3456324 500 88 0 9 3 4`  
- UPI-Zero gateway reply sent and confirmed. If ANY of the fields mismatch (the UPI-card number, amount or secret numbers), then the transaction fails. The other advantage of this flow versus USSD is that the shopkeeper can service multiple people in parallel. He does not have to complete one full transaction (inspite of phone network delays, etc) before starting to process another one. This is a huge advantage since shopkeepers have to do a lot of these.

### What needs to be done to make this possible

- **NPCI technical integration**  - NPCI will need to do technical integration of this new authentication mechanism (the card grid). Till today, the only way to use UPI/NPCI was through a SMS OTP and that is the current system they have built. This is the biggest reason why UPI needs a phone to work.  UPI-Zero+UPI-card will be an additional authentication that co-exists with NPCI's existing technology. If a user has come to UPI via the card grid, he will be served through the card grid authentication. If he signed up with his mobile number, then he will continue to use phone OTP.
   - If this is not built at the NPCI level (and instead done inside a single bank), then it has a high risk of failure of adoption by other banks. NPCI has already done the heavy lifting of consensus building - we believe we should leverage that. 
- **Bank support** - we can start off with one single bank. There is no risk of consensus by committee, since the infrastructure+authentication is at the NPCI/UPI level. Other banks can join one by one. There is no reason to roll this out with all banks at once.
- **Accounting and reconciliation** - whichever bank we work with should be able to dedicate resources to reconciling/accounting kirana stores that will need to be reimbursed (since they have fronted the money for wallet loading).
- **RBI approval** for e-kyc, Anti money laundering (AML) and compliance requirements.

# UPI-card and UPI-Zero proposal

- Sandeep Srinivasa (***sss@redcarpetup.com, +91-9810485533, Founder - RedCarpet.Cash*** ) 
-  Pravesh Biyani (***praveshb@iiitd.ac.in, +91-9716249729, Asst. Prof - IIIT Delhi***)






