---
layout: default
title: DailyMed Guide
description: A guide to using DailyMed as a data source for drug label information.
parent: Guides
nav_order: 1
---

# DailyMed Guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Getting started
DailyMed is the official provider of FDA **structured product label (SPL)** information (package inserts).

Check out the [DailyMed website](https://dailymed.nlm.nih.gov/dailymed/).

## Basic structure
Each SPL has a unique **set ID** that does not change over time.  However, with every update to an SPL, the **SPL ID** and **SPL version** can change.

Example label (note the set ID in the URL): [LISINOPRIL tablet](https://dailymed.nlm.nih.gov/dailymed/drugInfo.cfm?setid=7d6c31e2-b5a4-4279-8013-a8dad37ea73b)

There are links from this page to download the label info in PDF or XML format, as well as in the official label format.

### Main SPL sections
* NDC code(s)
* Packager
* Category
* DEA schedule
* Marketing status
* Date last updated
* Drug label information
    * Highlights of prescribing information
    * Table of contents
    * Boxed warning
    * Indications and usage
    * Dosage and administration
    * Dosage forms and strengths
    * Contraindications
    * Warnings and precautions
    * Adverse reactions
    * Drug interactions
    * Use in specific populations
    * Overdosage
    * Description
    * Clinical pharmacology
    * Nonclinical toxicology
    * Clinical studies
    * How supplied/storage and handling
    * Patient counseling information
    * Principal display panel
    * Ingredients and appearance


### Important features

| Feature name | Description |
| :----------- | :---------- |
| Package photos | Images of the drug packages, but not NDC-specific. |
| Drug photos | Images of the actual drug, associated with NDC. |
| Labeling archives | Download previous versions of SPLs. |
| RxNorm | Maps RXCUIs of different term types (TTY) to set IDs.<br/><br/>*NOTE: this mapping is specific to a **set**, not to a **product** or **package***. |
| Label RSS feed | Subscribe to updates to DailyMed labels via RSS. |
| Biochemical data summary | Links to [DrugBank](https://go.drugbank.com/) which is a pharmaceutical knowledge base. |
| NDC codes | All NDC codes associated with the SPL. |

## Available data

### REST API

DailyMed provides a REST API with the following endpoints.

The base URL is `https://dailymed.nlm.nih.gov/dailymed/services/` to which you can append the below endpoints. Some endpoints return either XML or JSON, while others only return XML.

| REST web service resources | Description |
| :------------------------- | :---------- |
| [/applicationnumbers](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/applicationnumbers_api.cfm) | Returns a list of all NDA numbers. |
| [/drugclasses](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/drugclasses_api.cfm) | Returns a list of all drug classes associated with at least one SPL in the Pharmacologic Class Indexing Files. |
| [/drugnames](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/drugnames_api.cfm) | Returns a list of all drug names. |
| [/NDCs](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/NDCs_api.cfm) | Returns a list of all NDC codes. |
| [/rxcuis](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/rxcuis_api.cfm) | Returns a list of all product-level RxCUIs. |
| [/spls](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_api.cfm) | Returns a list of all SPLs. |
| [/spls/{SETID}](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_setid_api.cfm) | Returns an SPL document for specific set ID. |
| [/spls/{SETID}/history](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_setid_history_api.cfm) | Returns version history for specific set ID. |
| [/spls/{SETID}/media](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_setid_media_api.cfm) | Returns links to all media for specific set ID. |
| [/spls/{SETID}/NDCs](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_setid_NDCs_api.cfm) | Returns all NDCs for specific set ID. |
| [/spls/{SETID}/packaging](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/spls_setid_packaging_api.cfm) | Returns all product packaging descriptions for specific set ID. |
| [/uniis](https://dailymed.nlm.nih.gov/dailymed/webservices-help/v2/uniis_api.cfm) | Returns a list of all UNIIs. |

<small>Source: [DailyMed web services](https://dailymed.nlm.nih.gov/dailymed/app-support-web-services.cfm)</small>

### Drug label downloads
[Drug label downloads](https://dailymed.nlm.nih.gov/dailymed/spl-resources-all-drug-labels.cfm) are available in zip file format, which contain images from the SPL and the entire SPL in XML file format.

Two different formats are provided depending on whether you want to stay on top of every incremental update, or just download the full release.
1. **Periodic updates** (monthly, weekly, or daily) of all drug labels.
1. **Full releases** of different types of drug labels.  Human labels are split across multiple zip files due to file size.
    * Human prescription labels
    * Human OTC labels
    * Homeopathic labels
    * Animal labels
    * Remainder labels

### Mapping files
[Mapping file downloads](https://dailymed.nlm.nih.gov/dailymed/spl-resources-all-mapping-files.cfm) are available in zip file format.
* SPL-RxNorm
* SPL-pharmacologic class
* Zip file metadata

### Indexing and REMS files
[Indexing and REMS file downloads](https://dailymed.nlm.nih.gov/dailymed/spl-resources-all-indexing-files.cfm) are available in zip file format.
* Billing unit
* Biologic or drug substance
* FDA-initiated compliance action - drug listing
* Pharmacologic class
* Product concept
* REMS and REMS indexing
* Substance
* Warning letter alert
