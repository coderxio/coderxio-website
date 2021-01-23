---
layout: post
title:  "Sorting RxNorm API results with Python: An arbitrary adventure"
author: Joey LeGrand
date:   2020-09-14 07:00:00 -0600
categories: rxnorm
tags: rxnorm api python
published: true
---
![meme](/assets/images/noone-meme.jpg)

I am sharing this because I jokingly told someone on a pharmacist Slack channel that it would be a good idea for a valuable, worthwhile pharmacy informatics resident project to sort all medications based on number of vowels and they took me seriously. I felt bad because I didn't want to waste that resident's time.  Obviously there is zero face value in this type of list, but part of me still thought it was kind of a good exercise to get familiar with the RxNorm APIs and some basic Python sorting and CSV exporting functionality. So, as a sort of penance, I wrote the script myself.

RxNorm has a ["Prescribable" API endpoint](https://rxnav.nlm.nih.gov/PrescribableAPIREST.html) that will only return prescribable drugs. Otherwise, you will get all drugs including veterinary medications and OTC medications. For those of you unfamiliar with RxNorm, it also classifies medications based on different levels called ["term types" or "TTY"](https://www.nlm.nih.gov/research/umls/rxnorm/docs/appendix5.html). For the purpose of this arbitrary example, I chose to go with the following:
- IN - ingredient
- MIN - multiple ingredient
- BN - brand name

As a "tiebreaker" (if two meds have the same number of vowels), I chose to do a secondary sort based on the number of letters in the word (or the length of the "string" in programming lingo). Then, once I sorted the list, I output the list in CSV so I could play around with it. You can open the CSV in Excel and filter out any of the TTYs you don't care about (i.e. if you only care about brand name drugs).

Here's a link to the CSV: [vowels.csv](/assets/data/vowels.csv)

In case you're wondering, the top meds in each category are:
- IN with 46 vowels and 147 letters (RXCUI = 2392632) - sodium 2-acrylamido-2-methyl-1-propane sulfonate/sodium acrylate/n-isopropylacrylamide/trimethyl(3-methacrylamidopropyl)ammonium chloride copolymer
- MIN with 509 vowels and 1543 letters (RXCUI = 1008785) - Streptococcus pneumoniae type 1 capsular polysaccharide antigen / Streptococcus pneumoniae type 10A capsular polysaccharide antigen / Streptococcus pneumoniae type 11A capsular polysaccharide antigen / Streptococcus pneumoniae type 12F capsular polysaccharide antigen / Streptococcus pneumoniae type 14 capsular polysaccharide antigen / Streptococcus pneumoniae type 15B capsular polysaccharide antigen / Streptococcus pneumoniae type 17F capsular polysaccharide antigen / Streptococcus pneumoniae type 18C capsular polysaccharide antigen / Streptococcus pneumoniae type 19A capsular polysaccharide antigen / Streptococcus pneumoniae type 19F capsular polysaccharide antigen / Streptococcus pneumoniae type 2 capsular polysaccharide antigen / Streptococcus pneumoniae type 20 capsular polysaccharide antigen / Streptococcus pneumoniae type 22F capsular polysaccharide antigen / Streptococcus pneumoniae type 23F capsular polysaccharide antigen / Streptococcus pneumoniae type 3 capsular polysaccharide antigen / Streptococcus pneumoniae type 33F capsular polysaccharide antigen / Streptococcus pneumoniae type 4 capsular polysaccharide antigen / Streptococcus pneumoniae type 5 capsular polysaccharide antigen / Streptococcus pneumoniae type 6B capsular polysaccharide antigen / Streptococcus pneumoniae type 7F capsular polysaccharide antigen / Streptococcus pneumoniae type 8 capsular polysaccharide antigen / Streptococcus pneumoniae type 9N capsular polysaccharide antigen / Streptococcus pneumoniae type 9V capsular polysaccharide antigen
- BN with 17 vowels and 49 letters (RXCUI = 1438498) - Preparation H Suppositories Reformulated Oct 2013

And here is the (heavily commented) script:

```python
# import the requests library 
import requests 
# import the csv library
import csv

# define vowels
vowels='aeiou'

# function to count vowels in a string
def count_vowels(string):
    count = 0
    # for every character in the string
    for s in string.lower():
        # if that character is a vowel (as defined above)
        if s in vowels:
            # increase the count by one
            count = count + 1
    # return the total count
    return count

# API endpoint
# NOTE: RxNorm has a "Prescribable" API endpoint for prescribable drugs only
URL = 'https://rxnav.nlm.nih.gov/REST/Prescribe/allconcepts.json?tty=IN+MIN+BN'

# send GET request and save the response as response object 
response = requests.get(url = URL) 

# extract data in json format 
data = response.json()

# get just the medication list of the data
meds = data['minConceptGroup']['minConcept']

# for each med, count the number of vowels and number of characters
# add that info to each med object
for med in meds:
    med['vowel_count'] = count_vowels(med['name'])
    med['length'] = len(med['name'])

# sort the medication list based on number of vowels (highest to lowest)
# secondary sort based on number of characters (highest to lowest)
sorted_meds = sorted(meds, key = lambda x: (x['vowel_count'], x['length']), reverse = True)

# print out the first 10 meds as a spot check
print(sorted_meds[:10])

# create a csv file called 'vowels.csv'
with open('vowels.csv', 'w', newline='') as csvfile:
    # define the column headers
    fieldnames = ['vowel_count', 'length', 'tty', 'name', 'rxcui']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    # write the column headers to the csv file
    writer.writeheader()

    # write a row to the csv file for each med in sorted_meds
    for med in sorted_meds:
        writer.writerow(med)
```

**CodeRx** is a collective of pharmacists and other healthcare professionals that have an interest, skill set, or passion in coding, data, or tech. Working on this project is the first of hopefully many projects where we can apply our knowledge towards something potentially cool and useful - and give others exposure to and experience with the techy side of healthcare along the way. If you're interested at all, follow along at [CodeRx.io](https://coderx.io/), check out our [GitHub repo](https://github.com/coderxio/dailymed-api), or join our [Slack channel](https://coderx.slack.com/).
