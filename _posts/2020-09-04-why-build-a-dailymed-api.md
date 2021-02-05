---
layout: post
title:  "Why build a DailyMed API?"
author: Joey LeGrand
date:   2020-09-04 07:30:00 -0600
categories: dailymed-api
tags: dailymed api
---
If you're reading this, you probably know what DailyMed is... but just in case you don't, I'll give a brief intro. [DailyMed](https://dailymed.nlm.nih.gov/dailymed/) is the official provider of FDA label information - package inserts or stuctured product labels (SPLs). The website provides a "standard, comprehensive, up-to-date, look-up and download resource of medication content and labeling found in medication package inserts" which is honestly very easy to use and quite useful as a clinician or as anyone who uses medication labeling information. 

What you might not know is that DailyMed also provides an [application programming interface (API)](https://en.wikipedia.org/wiki/API) so that web applications can digest and understand the same label information. For instance, if I take a label for a random medication called Revlimid and wanted to know the packaging information for each national drug code (NDC), I could go to [the packaging API endpoint](https://dailymed.nlm.nih.gov/dailymed/services/v2/spls/5fa97bf5-28a2-48f1-8955-f56012d296be/packaging.json). This isn't intended to be read by humans (though it is fairly straightforward), but it is super easy for a computer to understand this standard format (called [JSON](https://en.wikipedia.org/wiki/JSON)) and use it in a web application.  Packaging information is one of the several [DailyMed web services](https://dailymed.nlm.nih.gov/dailymed/app-support-web-services.cfm) provided by the site.

```javascript
data: {
  spl_version: 34,
  products: [
    {
      packaging: [
        {
          ndc: "59572-402-00",
          package_descriptions: [
            "100  in 1 BOTTLE"
          ],
        },
        {
          ndc: "59572-402-28",
          package_descriptions: [
            "28  in 1 BOTTLE"
          ],
        },
      ],
      active_ingredients: [
        {
          strength: "2.5 mg",
          name: "LENALIDOMIDE",
        }
      ],
      product_name_generic: "Lenalidomide",
      product_name: "Revlimid",
      product_code: "59572-402",
    },
    ...
  ...
```

Great - so DailyMed is awesome and already has an API.  So are we done here?

Not quite. You may notice, for instance that the API above provides `active_ingredients` but does not provide `inactive_ingredients`. However, [DailyMed's website](https://dailymed.nlm.nih.gov/dailymed/drugInfo.cfm?setid=5fa97bf5-28a2-48f1-8955-f56012d296be) clearly contains this information. This may be good enough for us humans... but computers need this to look more like the format above.

![Revlimid inactive ingredients](/assets/images/revlimid-inactive-ingredients.png)

One thing I haven't mentioned is that DailyMed also provides the ability to download every single product label in [XML](https://en.wikipedia.org/wiki/XML).  If we were to download the specific XML file for this specific Revlimid label on the [DailyMed drug label download page](https://dailymed.nlm.nih.gov/dailymed/spl-resources-all-drug-labels.cfm), and then find the specific section within the 9530 lines of XML that contains inactive ingredient information, it would look like the code below. You may notice some similarities between the picture of the table on the website and the structure of the XML - look for the inactive ingredient names in both.

```xml
...
<manufacturedProduct>
<code code="59572-402" codeSystem="2.16.840.1.113883.6.69"/>
<name>Revlimid</name>
<formCode code="C25158" codeSystem="2.16.840.1.113883.3.26.1.1" displayName="CAPSULE"/>
<asEntityWithGeneric>
    <genericMedicine>
        <name>Lenalidomide</name>
    </genericMedicine>
</asEntityWithGeneric>
<ingredient classCode="ACTIB">
    <quantity>
        <numerator value="2.5" unit="mg"/>
        <denominator value="1" unit="1"/>
    </quantity>
    <ingredientSubstance>
        <code code="F0P408N6V4" codeSystem="2.16.840.1.113883.4.9"/>
        <name>LENALIDOMIDE</name>
        <activeMoiety>
            <activeMoiety>
            <code code="F0P408N6V4" codeSystem="2.16.840.1.113883.4.9"/>
            <name>LENALIDOMIDE</name>
            </activeMoiety>
        </activeMoiety>
    </ingredientSubstance>
</ingredient>
<ingredient classCode="IACT">
    <ingredientSubstance>
        <code code="3SY5LH9PMK" codeSystem="2.16.840.1.113883.4.9"/>
        <name>ANHYDROUS LACTOSE</name>
    </ingredientSubstance>
</ingredient>
<ingredient classCode="IACT">
    <ingredientSubstance>
        <code code="OP1R32D61U" codeSystem="2.16.840.1.113883.4.9"/>
        <name>MICROCRYSTALLINE CELLULOSE</name>
    </ingredientSubstance>
</ingredient>
<ingredient classCode="IACT">
    <ingredientSubstance>
        <code code="M28OL1HH48" codeSystem="2.16.840.1.113883.4.9"/>
        <name>CROSCARMELLOSE SODIUM</name>
    </ingredientSubstance>
</ingredient>
<ingredient classCode="IACT">
    <ingredientSubstance>
        <code code="70097M6I30" codeSystem="2.16.840.1.113883.4.9"/>
        <name>MAGNESIUM STEARATE</name>
    </ingredientSubstance>
</ingredient>
...
```

So we now know that the information on a given human-readable DailyMed label website is also stored in a somewhat structured format in computer-readable XML that is also provided on a regular basis by DailyMed. This is probably good enough for a lot of people that know about this XML and slog through it to find what they need for research or other purposes.  But the file we downloaded to get the code above might change next month... or a new medication label could be uploaded to DailyMed tomorrow and what if we need inactive ingredient information from that?

What if we wanted to make the inactive ingredient information as easy to access as following a web link to some JSON like we can do for active ingredients? We could certainly ask DailyMed to do this... or we could do it ourselves! Inactive ingredient information is just one example of the type of data that is readily available in a product label, but (at least to my knowledge) not easy to find in an up-to-date, structured format elsewhere. There are certainly other things in a DailyMed medication label that healthcare professionals could benefit from if they were made available in a structured way to a web application. We plan on starting with inactive ingredients as a proof of concept and then going after other things. What medication product label information would you want to be available via an API?

---

**CodeRx** is a collective of pharmacists and other healthcare professionals that have an interest, skill set, or passion in coding, data, or tech. Working on this project is the first of hopefully many projects where we can apply our knowledge towards something potentially cool and useful - and give others exposure to and experience with the techy side of healthcare along the way. If you're interested at all, follow along at [CodeRx.io](https://coderx.io/), check out our [GitHub repo](https://github.com/coderxio/dailymed-api), or join our [Slack channel](https://join.slack.com/t/coderx/shared_invite/zt-5b8e9kr4-PsKAVe4crGmECQyyxDIJgQ).
