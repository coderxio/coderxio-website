---
layout: post
title:  6 ways your prescription could get messed up
author: Joey LeGrand
description: The medication use process is complex and fragile. There are many steps along the way to getting your prescription filled correctly, and getting the right prescription at the right time often depends on how accurate your med list is. 
image: /assets/images/not-how-this-works.jpg
date:   2021-04-27 06:00:00 -0600
categories: prescriptions
tags: surescripts medrec cpoe hie
published: true
---

The medication use process is complex and fragile. There are many steps along the way to getting your prescription filled correctly, and getting the right prescription at the right time often depends on how accurate your med list is. Often, many disparate systems and clinicians need to work together correctly to keep your med list and prescriptions accurate. The vast majority of the time, everything goes right, but it takes a lot of careful effort, and there are still several places where things could fall through the cracks.

![That's not how this works. That's not how any of this works.](/assets/images/not-how-this-works.jpg)

## Outpatient med rec
Outpatient medication reconciliation (or med rec) is where your doctor or nurse asks what medications you are currently taking during a clinic visit. They are looking for potential drug interactions or adverse effects and also trying to get clues to your medical history. You might misremember a medication name and the incorrect med gets added to your med list. You might have a short-term topical cream on your med list from 2 years ago that nobody has taken the initiative to remove and today your PCP accidentally refills it and you pick it up with your other meds.

## Inpatient med rec
Inpatient med rec is like outpatient med rec, but - you guessed it - inpatient. There’s admission med rec where you get asked what meds you take and the last time you took them, and then a provider decides if they need to continue those meds while you are in the hospital. Hospitals have formularies (lists of preferred medications for financial, operational, or clinical reasons) - so while you may be taking brand name Crestor at home, you might get an equivalent dose of generic simvastatin while you’re admitted. Then, during discharge med rec, a resident may accidentally send a script for simvastatin to your pharmacy instead of the brand name Crestor you’ve been taking.

## Health information exchange (HIE) between hospitals
More and more, hospitals are able to share health records - including medication lists. For this to work perfectly, the medications from these data sources need to have a common identifier (i.e. RxNorm) so that hospital A and hospital B know they are both talking about the exact same medication. Sometimes, even though the two hospitals are connected, the medication is missing that common identifier. This means the clinician receiving the information needs to do manual mapping of these medications to local products in their EHR - introducing room for human error which is highly dependent on the quality of the data entry user interface of their specific system.

## Fill history / claim history data feed
Companies like Surescripts provide a data feed of your prescription fill history at pharmacies and your prescription claim history with your pharmacy benefits manager (PBM) to hospitals as a paid source of information for med rec (see sections above for what med rec is). Many pharmacies and PBMs send structured medication data (with NDCs or RxNorm codes and even structured sigs / instructions); however, sending structured data is not required by Surescripts. If an entire pharmacy chain or PBM decides to not send structured medication data, this can result in data entry errors similar to the HIE section above or a loss of clinician trust in this otherwise valuable data source.

## Computerized provider order entry (CPOE)
Even if everything above goes according to plan, there is still a chance that an ordering provider could make an error when entering the prescription in the system. If using an EHR, this is called computerized provider order entry (or CPOE). Errors could include picking the wrong strength, entering incorrect instructions, or putting information in the wrong fields - among other things (see image above). CPOE is well-studied and I’m not going to go into detail about it here, but there is definitely still room for improvement in terms of human-computer interface design here. In some EHRs, if a script is ordered incorrectly one time and not corrected, it can perpetuate the error on the med list for future refills and med rec.

## Pharmacy system
The final safety net between you and your prescription is the pharmacy and whatever pharmacy management system they are using. Electronic prescriptions can automatically show up in a pharmacy’s work queue, but many elements of the prescription require manual review and data entry by the pharmacy staff. Sometimes an ordering provider will choose a particular strength, but put a note in the comments to dispense a different strength (see CPOE section above). If medication product information or instructions aren’t structured, they need to be transcribed by the pharmacy staff into products and instructions understood by their system. A provider may have electronically cancelled the prescription after it was sent, but the hospital may not have NCPDP SCRIPT CancelRx transactions configured so the script still gets filled.

## Summary
The next time you pick up a new or existing prescription at your pharmacy (or in your mailbox), be cognizant of all the steps that have gone into getting it to your hands. Be a champion of your own med list and work with your provider and pharmacist to ensure it is correct at every visit. As I mentioned, the vast majority of the time everything works and the right medications get to the right people at the right time - but it takes the care and vigilance of clinicians and patients to make that happen.

Technology can’t replace the human engagement in this process, but incremental improvements like carefully analyzing user interfaces critical to each step of this process, sending more structured medication information across interfaces, and widespread implementation of transactions like CancelRx could make the existing system more reliable, useful, and trustworthy.

---

**CodeRx** is a collective of pharmacists and other healthcare professionals that have an interest, skill set, or passion in coding, data, or tech. If you're interested in learning more, follow along at [CodeRx.io](https://coderx.io/), check out our [GitHub repo](https://github.com/coderxio/dailymed-api), or join our [Slack channel](https://join.slack.com/t/coderx/shared_invite/zt-5b8e9kr4-PsKAVe4crGmECQyyxDIJgQ).
