---
layout: post
title:  Modernizing pharmacy drug procurement with APIs
author: Kent Bridgeman and Joey LeGrand
description: What would a world look like if modern API technology was applied to pharmacy drug procurement?  We’re glad you asked.  We put together some before and after workflow diagrams of what the current process is and how it could be improved with APIs.
image: /assets/images/drug-procurement-header.jpg
date:   2021-01-25 05:30:00 -0600
categories: drug-procurement
tags: edi api wholesaler inventory shortage
published: true
---

![Drug procurement header](/assets/images/drug-procurement-header.jpg)
*Photo by National Cancer Institute*
{: .fs-2}

People may assume just because Amazon exists and has made shopping online effortless for consumers, that this has by now spread to all other industries that depend on buying things on a regular basis.  In the case of pharmacy drug procurement, this is certainly not the case.  One of the reasons that e-commerce websites like Amazon are so fast, up-to-date, and user-friendly is that they use something called an **application programming interface (API)** to provide instantaneous machine to machine communication.  It is what allows a phone application to exchange information with Amazon and place an order through various requests.

APIs are built on a standardized foundation of requests and responses about the state of objects. There’s different kinds of requests you can make to an API, but the most common are **GET and POST requests**. If we use an API example from another industry important to commerce - the shipping industry - applications can make GET requests to check prices on shipping (the response would be a list of prices) and POST requests to purchase shipping labels (the request would actually create an order, and the response would be a confirmation of the order and any details specific to the label).  Also, these APIs are made available to third party websites so other businesses can integrate with them - which is why it is so easy to check tracking information regardless of what company is shipping your products or why Amazon can generate your UPS return label if you are sending back a product.

So what do pharmacies use?  Currently, the main way drugs are purchased by pharmacies from wholesalers is through a method called **electronic data interface (EDI)**.  If we think of an API like a phone conversation, EDI is more like sending a fax.  A key difference is that EDI is a one-way message with typically no automatic response.  Another key difference is that while an API request and the object the request is about are bound together, an EDI is just a message with no real association to the objects referred to within the message.  In other words, the EDI itself does not know anything about the product you are ordering, but an API would have access to all the available details about that product due to tight integration with the data model.

What would a world look like if modern API technology was applied to pharmacy drug procurement?  We’re glad you asked.  We put together some before and after workflow diagrams of what the current process is and how it could be improved with APIs.  Long story short, there could be a lot less time spent by a buyer doing manual work interacting with various systems, automatics substitutions for products on drug shortage, and possibly even lower costs.

## Definitions

EDI
: electronic data interface

API
: application programming interface

PO
: purchase order - order sent from the pharmacy

PAR
: periodic automatic replenishment levels - minimum quantity of a product needed on hand

NDC
: national drug code - in this case, identifies a specific package of a drug product

DC
: distribution center - location where manufacturer stores drug products before they are shipped to pharmacy

## Current state workflow with EDI

This is a rough estimate of how pharmacy buyers currently go through a normal ordering workflow, and is certainly not meant to represent how every pharmacy handles this.  There are many differences in vendors, wholesalers, and internal workflows that could result in variations.  In this example, at least one product is unavailable or on drug shortage.

![Drug procurement current state with EDI diagram](/assets/images/drug-procurement-current-state-edi.jpg)

*   Inventory system automatically generates a purchase order (PO) based on current on-hand quantity of products with specific national drug codes (NDCs) and defined minimum quantity of product needed on hand (also known as PAR)
*   Buyer reviews the automatically generated PO within inventory system and submits to wholesaler system (EDI 850)
*   Buyer logs in to wholesaler web portal to verify PO was received and information is accurate
*   Buyer places PO to wholesaler
*   In the event of a shortage, some NDCs will not be fulfilled by the wholesaler when the order is received and the invoice is available a day or more later
*   Buyer logs back into wholesaler web portal to search for therapeutically and operationally (i.e. same volume for mixtures) equivalent NDC with stock at the distribution center (DC) - potentially multiple times throughout the day if all equivalent NDCs are out of stock
    *   Local inventory system typically has built in mapping to know what products would be equivalent; however, these systems aren’t typically interfaced with the wholesaler
    *   Instead of utilizing the separate systems, buyer typically just has to know which products are equivalent and manually search by keyword or NDC to find them on wholesaler website
*   Buyer eventually finds equivalent NDC with stock listed as available at DC, and submits second order
*   Another day later (or more if the previous steps have to be repeated more than once), when the new NDC finally arrives, the NDC that was originally on shortage still shows up as below minimum quantity in inventory system, which means the following day it will show up again on the automatically generated PO from the inventory system
*   Buyer updates preferred NDC in inventory system so that original NDC is not automatically added to generated PO the following day (since it is on shortage)

## Future state workflow with API

Taking the same scenario as above (at least one product is unavailable or on drug shortage), but applying a modern API workflow, we can see how much less interaction is required by a buyer to achieve the same end result in likely much less time overall.

![Drug procurement future state with API diagram](/assets/images/drug-procurement-future-state-api.jpg)

*   Inventory system automatically generates a list based on current on-hand quantity of products with specific national drug codes (NDCs) and defined minimum quantity of product needed on hand (also known as PAR)
*   Inventory system makes GET request to wholesaler via API, which would return the following information from the manufacturer:
    *   Distribution center (DC) inventory count for each NDC
    *   Current pricing information for each NDC
*   For any NDC returned with zero (or very low) inventory count, the inventory system would check its own already existing database for all equivalent NDCs, and make another GET request to wholesaler via API for that entire list of equivalent NDCs
    *   The inventory system could be configured to periodically make this GET call multiple times a day to monitor inventory availability in the DC throughout the day and notify buyer if an NDC becomes available
*   Now the list of NDCs in our order is completely comprised of either:
    *   Preferred NDCs with stock at the DC
    *   For any NDCs unavailable or on shortage, a list of alternate NDCs with pricing and inventory information for the buyer to review and quickly select
    *   For any NDCs with no available alternatives, a reliable indicator that the buyer will need to find that product elsewhere
*   Based on the response to the initial GET request, the inventory system knows that the original NDC is on shortage and replaces preferred NDC (with a flag for buyer approval)
*   Buyer reviews all changes in one sitting and submits order to wholesaler via a POST request on the API, which contains at minimum the NDCs and order quantities
*   Buyer receives nearly instantaneous response back from wholesaler via API acknowledging receipt and confirmation of order

## Future state workflow with multiple APIs

Everything would be the same as the API workflow above, but with multiple wholesalers all using an API (ideally the same API based on standards), an inventory system could make requests to multiple wholesalers at the same time and find the least expensive option and / or quickly find substitutions for products unavailable at a main wholesaler.

![Drug procurement future state with multiple APIs diagram](/assets/images/drug-procurement-future-state-multiple-api.jpg)

## Conclusion

The goal of this post is not to point fingers, but to make pharmacy employees start thinking about how their workflows could be more effective by applying technology they are familiar with from other industries.  We have shown that APIs have the potential to reduce unnecessary inefficiencies in the pharmacy drug procurement process by modernizing the interfaces between inventory systems and wholesalers.  The example we used is relatively simple, and did not even cover how APIs could improve more complex 340B or 503B purchasing workflows.

Any significant change will require buy-in from both inventory system vendors and wholesalers, but the industry awareness will need to start with pharmacy customers who know there can be a better way and start asking about it.  Time saved dealing with these tedious processes can be instead devoted to patient care, and more reliable ordering could mean patients get their medications sooner -- especially during times of drug shortage.  Now that we have pointed out one area where APIs can add value in this space, what other pharmacy workflows could benefit from this type of real-time machine to machine communication?

---

**CodeRx** is a collective of pharmacists and other healthcare professionals that have an interest, skill set, or passion in coding, data, or tech. If you're interested in learning more, follow along at [CodeRx.io](https://coderx.io/), check out our [GitHub repo](https://github.com/coderxio/dailymed-api), or join our [Slack channel](https://coderx.slack.com/).
