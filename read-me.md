---
layout: page
title: test
---

> Written by Donato Onorato for file `naics_isic.py`.
>
> July 11, 2017.

hpcc-path: `/home/mktg/onoratod/projects/RAs/onoratod/python-scripts/naics-isic/`

# **Merging IFR and InfoGroup Test**

## Overview

The goal of this code was to test how we could merge the IFR robotics data and the InfoGroup firm characteristics data (sales volume, employment size, etc).

The obvious thing to do was use the IFR **ISIC codes** and match them to InfoGroup's provided **NAICS codes** using **NAICS-ISIC crosswalks**.

The test was performed on InfoGroup 2007 data from WRDS. The output of the tests can be found in the `sample-tests` folder.

## Implementation

To implement the test merge, I used a 10% sample of the InfoGroup data (approx 1.3 million observations).

The next thing to note is that, there exist several crosswalks between NAICS and ISIC Rev. 4. This is because NAICS codes were updated in the years: 2007, 2012, 2017.

To deal with this inconsistency we will do several mappings, starting with the 2007 crosswalk and subsequently using the 2012 and 2017 crosswalks.

So, the first thing I do is initialize three dictionaries, which contain the mappings from NAICS to ISIC for each year 2007, 2012, 2017. I save these dictionaries to the directory as `.npy` files and then read them in. These dictionaries provide **1:m** mappings from NAICS to ISIC, we will keep track of all of potential matches.

The next step is to try to assign each NAICS in the sample an ISIC code using the dictionaries. Starting with 2007 then moving onto the others (we will only keep track of the maximum number of matches in 2007, so if there are 9 matches for one NAICS in 2007, then we will keep track of 9 matches for every other NAICS even if they don't have 9 matches).

## Performance

For more stats about how the tests performed see the `sample-test` folder.

In most cases after the 2007 crosswalk around **8%** of observations are unmatched (a large majority of these are either unclassified, 999990 codes, or missing the NAICS code, -999). This amounts to **72 NAICS codes** including the unclassified codes and the missing code.

After the 2012 crosswalk, all that remains unmatched are the 999990 codes and the missing NAICS codes.

As expected, the 2017 crosswalk can't match unclassified or missing NAICS codes, so we end up with **2%** of the data having an unmatched ISIC code. However, **92%** of the unmatched codes are simply the 99990 unclassified codes. This means that only **0.16%** of the data is actually missing an NAICS codes.
