# Table of Contents


1. [Introduction](#1-introduction)
<!--- Here I'll explain what this document is all about, which is all about auto-merging, and how it will help the future analysts to focus more on prox audits that require more in depth research. I need to create the motivation on what to expect in this document and how we will be slowly curating some theoretical and technical aspects that the reader should know before he/she can understand the fundamentals of auto-merging process itself, like: We'll tackle the primary identifiers used to determine information about towers (FAA and FCC) and show what they signify and where we can get those information (maybe we can google search some of the definition of terms and crash courses about these), talk about the proximity audits in Sherlock's perspective, talk about the proximity audits in Skeletor's perspective, talk about the anatomy of a group or single prox audit, talk about how prox audits can be queried from the backend tables, talk about auto-merging and how it will help us in implementing automation jobs, --->
2. [TowerSource's Data Source Overview](#2-towersources-data-source-overview)
   1. [Company data](#i-company-data)
      <!---a.) Outreach (Show an example of email sent to the companies and the example raw tower sheet we received from them, also say that not all companies are reporting complete data), b.) Web Scraping (Show websites where they have site locators in a form of maps or something where web scraping can be performed)--->
      1. [Company Tower Sheet from the Tower Company](#a-company-tower-sheet-from-the-tower-company)
      2. [Company Tower Sheet by Outreach](#b-company-tower-sheet-by-outreach)
      3. [Web Scraping](#c-web-scraping)
   3. [FCC-ASR](#ii-fcc-asr)
      <!-- Show the website, link the website, describe what the website is all about, show an example of a complete tower information. --->
   4. [FAA](#iii-faa)
      <!-- Show the website, link the website, describe what the website is all about, show an example of a complete tower information. --->
      
3. [Towersource Proximity Audit Overview](#3-towersource-proximity-audit-overview)
   1. [Overview](#i-overview)
      <!-- From the previous section, we talked about the Tower Assets' sources. Now, the Data Analysts should now perform some auditing to reconcile records in the database coming from these sources regarding which pertains to the same tower and otherwise. Since we capture data from these different sources, it is probabilistic to think that a single tower site will show up to these three different sources, one way or another. In the world of Towersource, if a tower asset/record, say, coming from the company pertains to the same tower showing from FCC-ASR and/or FAA's website, then the analyst should "merge" the records and create a singular record that will capture all of the demographics and techinical details of that said tower as complete and accurate as possible. But if a set of records pertain to different towers, then the analyst should not merge any of these records and just to "Confirm Correct" that each records are independent and different from each other, and then "Continue" to the next set of records to audit. But what logic should be followed on how to structure these "set of records" that should be grouped together for the analyst to look and do his/her further research? Also, what platform will these audits show up? As of the moment, we have the "Sherlock" UI to see all audits that the analyst should research and resolve (Show Sherlock), but since we're building the newer platform now in Superblocks these audits will be migrated there. In the general world of TowerSource, these audits can be determined through the "proximity audit". Here, I should define Proximity audits and the basic overview logic behind it. I should make it a point that it is very important to have the geographical coordinates shown by a specific tower site coming from either the Company', FCC-ASR's or FAA's website to determine which of the records should be grouped together and be further analyzed by the analyst simultaneously. A single "grouped" records based on proximity audit's logic can be called as a single "audit" or "group/grouping". As we load newer tower information coming from these different sources,  But what are the parts of a single "audit" or "grouping"?---> 
   2. [Anatomy of Proximity Audit](#ii-anatomy-of-proximity-audit)
      1. [Proximity Audit from Sherlock's view](#a-proximity-audit-from-sherlocks-view)
         <!-- Just show an example proximity audit and point out which is the reference/focus record and which is/are the associated record/s. --->
      2. [Proximity Audit from Skeletor's view](#b-proximity-audit-from-skeletors-view)
         <!-- What table should give you the information about which if the focus and which are the respective associated records? What table should be used to join this proximity audits table to determine a more in depth tower information for each. Show here and link the SQL I wrote to get these information. Put a disclaimer that we will not be using delving into the "dimensions" table (i.e., manager_table, operator_table, etc.). We will end this section by showing the whole SQL and the snippet of the output (without the AGL thingies yet). --->
         
4. [Auto-Merging's Designed Process Overview](#4-auto-mergings-designed-process-overview)
<!--- Here, I will just introduce again the auto-merging process and the goal of creating an automated process for the merging process so that the analyst will only focus more on "audits" or "groupings" where further human intervention is required (i.e., further research, further traversing of the maps, further inquiries, etc.). I will discuss here that we will be using as a 'primary identifier' the FCC-ASR and FAA study number to determine one tower from another. These two ingredients will help us determine which focus/reference record should be merged to their respective associated record, and which shouldn't be merged and just do nothing with the records in a grouping or audit. And then from these identifiers, we can create different combination scenarios for FCC-ASR or FAA on how these two ingredients would show up in a grouping or audit. We will call these combination of scenarios as "cases". For the first implementation of the auto-merging process, we devised the 5 major cases: blablablabla --->

5. [Auto-Merging's High Level Logic](#5-auto-mergings-high-level-logic)
   <!--- Here, I should mention that this process can be divided in to three major chunks of logic: The Looking for Merging candidates, the meats-n-potatoes process of Case X, the maintenance logic. And then describe briefly what each chunks of logic represents and what to expect for each one of which. --->
   
6. Auto-Merging Process' Database Anatomy
   <!--- I think it is better if I'll enclose each table in a tabular information as presented for each sub items of chapter/section 6 --->
   1. Prox Audits Table
      <!---Here, I should introduce the table name and what should it consist. I need to say that this table is the input table for each Case. So for Case 1, the input table should be the prox_audits table ran by my query.--->
   2. Merging Candidates
      <!---Introduce the name of the tables produced by this chunk of logic and what kind of records should be housed by each table. I should say that "if we continue case 1's process, it should producs tables X and Y". --->
   3. Further Filter & Merging Process
      <!---Introduce the name of the tables produced by this chunk of logic and what kind of records should be housed by each table. I should say that "if we continue case 1's process, it should producs tables X and Y". --->
   4. Maintenance Process
    <!---Introduce the name of the tables produced by this chunk of logic and what kind of records should be housed by each table. I should say that "if we continue case 1's process, it should producs tables X and Y. And then at this point, Table Z will be the input table for Case 2 to kick off, and then the same process continues for each Cases". --->
   
7. Elaborated Auto-Merging Process (Algorithm)
   1. Table Metadata
      <!--- Information about each columns in prox_audits table. --->
   2. Python Packages
      <!--- Just enumerate all of the python packages I will be using and then define each of the packages but I will be putting the documentation Cited in the bibliography but hyperlinked in the word "Documentation" as part of this section's paragraphs --->
   3. Preliminary Part
      <!--- Here, I will present the loading of the data, agl difference, geodesic, future warnings, caching, scraping, merging, etc. Any logic or defined functions in my code that is not part of the three major chunks of auto-merging process. At the end of this part, tell the reader to look at the whole code to appreciate the placement of each defined functions in the code. --->
   4. Case 1 Logic
      <!--- I can mention that this case would most probably play its role more as we load more tower sheets from the companies. Nonetheless, mention the logic behind this case step-by-step and as clear as possible--->
      <!--- For each chunks, I should show the code.--->
      1. Merging Candidates
      2. Further Filter & Merging Process
      3. Maintencance Process
      4. Example
         <!--- Show an example grouping that made it through this case successfully --->
   5. Case 2 Logic
      <!--- I can mention that this case would most probably play its role more as we load more tower sheets from the companies. Nonetheless, mention the logic behind this case step-by-step and as clear as possible--->
      <!--- For each chunks, I should show the code--->
      1. Merging Candidates
      2. Further Filter & Merging Process
      3. Maintencance Process
      4. Example
         <!--- Show an example grouping that made it through this case successfully --->
   6. Case 3 Logic
      <!--- I can mention that this case would most probably play its role more as we load more tower sheets from the companies. Nonetheless, mention the logic behind this case step-by-step and as clear as possible--->
      <!--- For each chunks, I should show the code--->
      1. Merging Candidates
      2. Further Filter & Merging Process
      3. Maintencance Process
      4. Example
         <!--- Show an example grouping that made it through this case successfully --->
   7. Case 4 Logic
      <!--- For each chunks, I should show the code--->
      1. Merging Candidates
      2. Further Filter & Merging Process
      3. Maintencance Process
      4. Example
         <!--- Show an example grouping that made it through this case successfully --->
   8. Case 5 Logic
      <!--- For each chunks, I should show the code--->
      1. Merging Candidates
      2. Further Filter & Merging Process
      3. Maintencance Process
      4. Example
         <!--- Show an example grouping that made it through this case successfully --->
   9. Whole Code
       <!--- I don't need to paste the whole code here. What I can do is just link the file with the whole code here. I would say that the code provided is for the jupyter notebook environment to be ran. I will yet to put the code that can be ran from other IDEs like spyder or pycharm or the like. -->
      
8. [Future Plans](#8-future-plans)
   <!--- In the future, we are to expect that we will be seeing more opportunities to expand the functionality of the auto-merging process from the five major cases we focused on. As of now, we are studying the possibility of having Case 6 (and then just give an overview on how it looks like and an example). --->

9. [References](#9-references)
     <!---I can create a numbering style (like in RRL) for each parts in the main documentation and then cited in this chapter. --->
     <!---FCC-ASR Website, research papers where FCC-ASR has been released or reviewed, FAA's website, research papers where FAA has been released or reviewed, packages used in Python (each packages should be cited using their documentation (can be a URL) --->

---
# 1. Introduction

[Towersource](https://www.towersource.com/)[^1] by **Ookla** is a large online database of vertical assets, like cell towers. It acts as a centralized directory that connects tower owners with tenants (such as moibile carriers) who need to lease space. It's like the Zillow for cell towers. If you own a cell tower, you can list it for sale or rent. If you're a mobile phone company (like T-Mobile or Verizon) and need to put antennas somewhere, you use TowerSource to search for the perfect spot. It helps companies find locations, see what competitors are doing, and manage their properties, all using a single, up-to-date database run by Ookla. 

Ookla's DQA Team takes its role in the perspective of Towersource database management and auditing. As part of our team's initiatives, we are to migrate the legacy Towersource system, which is the  "Sherlock" User Interface and "Skeletor" database, into a much newer platform, in the name of [Superblocks](https://docs.superblocks.com/)[^2], in order to refurbish and improve the process itself with the goal of automating multiple facets from the legacy Towersource system.

One of the aspect that our team have deliberately focused into automating is what we call as the **Auto-Merging process**. This automated process is programmed to audit and perform automatically the **merging process** from the vertical assets needed to be analyzed and researched in our Towersource's database. This way, it will significantly diminish the volume of assets that need to be audited by the DQAs, which will also help into the reallocation of their efforts to focus more into auditing vertical assets that requires more in-depth research before committing such information into our database for the market's consumption.

For this techical documentation, it will solely be dedicated to rigorously discuss the Auto-Merging process which is implemented as part of the **TowerSource Automation Project** which is to be deployed in the Superblocks platform, as mentioned previously. To give more benefit for the readers of this documentation, we will not delve instantly into the Auto-Merging process. In order to build some intuition and knowledge in this process, we will be discussing first some basic prerequisite frameworks about Towersource in general. This way, the reader will be able to understand some jargons used in this document and will be able to connect the dots seamlessly. We will delve first into the data sources in building the Towersource database, which will be followed by an overview of the proximity audits and how it looks like in the legacy Towersource system. Next, we will simply discuss the anatomy of an "audit" to know its parts and the information that the user should expect to see for each vertical assets. After these prerequisites, we will then be slowly introducing the overview of the Auto-Merging process. As we go deeper into this, the reader is to expect learning the step-by-step procedure of the said process which is to be supplemented by some programming aspect for technical readers. At the end, we will be discussing some future plans to motivate some perspective on what should we expect on how the said process will venture more in the future.

The reader should expect to learn the prerequisites of Towersource process in Sections 2 and 3. After these, the reader should expect to gradually learn the Auto-Merging process itself in Sections 4, 5, 6, and 7. Lasly, Section 8 will be the foreword of this document which will tackle the future plans for the said automation process.

As a disclaimer, this document will not entail the discussion of the totality of each TowerSource modules implemented in Superblocks. Auto-Merging process is expected to kick off after all necessary process of Towersource ran and before the DQA's auditing will take place. To know more about the architecture and backend development of the TowerSource in Superblocks platform prior to the processing of Auto-Merging job, please refer to this (*just a placeholder here to add Ar Jay's Documentation*) documentation. This document is also not the main document to be used as reference by the readers to understand the business rules and logic behind TowerSource in depth. The theoretical framework discussed in this document are the prerequisite information that the readers should know before digging into the world of Auto-Merging process. Nonetheless, we hope that this document will shed light into the reader's perspective into understanding more of our initiatives for the betterment of Towersource.

---
# 2. Towersource's Data Source Overview

For this section, we will be discussing how we collect data into building the rich database of Towersource. Generally, the said system is collecting data from the tower company itself, from Federal Communications Commission's Antenna Structure Registration (FCC ASR), and Obstruction Evaluation/Airport Space Analysis (OE/AAA). Each data source's overview will be discussed in this section. 

## i. Company Data

One of Towersource's data source is the Company data or what we call as the "Company Tower sheets". Sometimes, tower companies will be reaching out to us to have their Tower Assets be reflected in the interface of Towersource. Otherwise, there are times too where the DQA team will be performing some "Outreach" activities where an analyst of the team will be reaching out various tower companies. If the Company Tower Sheets couldn't be collected by eitherways, there are times where the DQA team will perform some Web Scraping methodology if the Tower Company's tower assets are publicly available and listed in their official websites (*i.e., most of the time in a form of an interactive map, if not shown as tabular data in the company's official website*). In this section, we will be showing these briefly with some examples each to visualize what a company tower sheet looks like and how to perform each of the said methods.

### a. Company Tower Sheet from the Tower Company

Tower Companies show interests into wanting their tower sites be reflected into Ookla's Towersource web interface. This way, it will help these Tower Companies find locations, , see what competitors are doing, and manage their properties. For this to happen, there are Tower Companies who reaches out to our team to make their Tower Assets be reflected in Towersource which is mostly in the form of an email. Shown below is an example exhibiting this: 


![company reaching out](document_images/company_reach_out.png)


> Here, Arcola Towers directly Reached out to our team wanting to reflect in Towersource's interface their current updated Tower Assets listing.

<br>
<br>

Now shown below is an example contents from the said tower sheet:


![example contents](document_images/company_reach_out2.png)


> Note that Tower Companies have their own styles and formatting of sending their tower listings to us. Some companies might report fields pertaining to elevations in meters or feet or whatnot. Some companies will report ASR and/or Study Number but some will not. Some companies will report the geographical coordinate locations of their towers in decimal degrees or in Degrees-Minutes-Seconds or in Degrees and Decimal Minutes, etc. In legacy Towersource, the DQA analysts make sure to preprocess these information manually to standardize the reported data coming from different companies before uploading these into the database for further staging. In Superblocks Towersource, this preprocessing stage will be automated.
<br>

### b. Company Tower Sheet by Outreach

If Tower Companies aren't reaching out to us whenever they have some updates with their Tower Assets listing, DQA team has the responsibility to do some "Outreach" methodology which is done every quarter of the year. Here, we are to reach out to various Tower Companies asking if they can provide us their current and most up-to-date Tower Assets listing. Mostly this is done through email form, as shown below: 


![company outreach](document_images/company_out_reach.png)



> Here, we provide our standardized format that the Tower Companies should follow whenever they will be providing us their most up-to-date Tower listing.

<br>


### c. Web Scraping

Sometimes Tower Companies would not be sending us their updated Tower listing and they would not be responding to our Outreach as well. If so, as a last resort, we can check the official web page for these Tower Companies to see if they have publicly available information about their Tower Assets. Most of the time, they showcase their Tower Assets through some interactive maps. Sometimes, they list their tower assets in a tabularized manner. If so, we can utilize these publicly available information but it would be laborious to do it manually especially if the tower company have hundreds or thousands of tower assets. This is when web scraping methodology will help into getting these information in an instant. Example shown below from **Titan Towers**:


![web scraping 1](document_images/web_scrape1.png)


![web scraping 2](document_images/web_scrape2.png)


![web scraping 3](document_images/web_scrape3.png)


Here, we can see that Titan Towers has an interactive map where each pinned points can be navigated to drill further the tower's demographics. To web scrape this example, we can check first, using developer's tool, the Network and Response for each items that would show up in the tool. This way, we are somewhat investigating the structure of the website itself for us to carry out the appropriate web scraping method we can use. For this case, since the information for each pinned points in the map are pulled through Direct API interception, we can just easily use the [requests](https://requests.readthedocs.io/en/latest/)[^3] python library package to scrape the desired information.


> Note that each website are built differently. That's why it is important to inspect the website's structure or use developer's tool to see the appropriate method of scraping the said website. Sometimnes you might use python library packages like [Selenium](https://selenium-python.readthedocs.io/)[^4] whenever the tower information are stored dynamically or whenever you want to perform browser automation, or one can use [BeautifulSoup](https://pypi.org/project/beautifulsoup4/)[^5] (in conjunction with requests or Selenium) to statically parse HTML/XML and extract specific information from it.

<br>
<br>

## ii. FCC-ASR

**Antenna Structure Registratrion (ASR)** is a program and an online database that requires the owners of certain tall antenna structures to register them with the **Federal Communications Commission (FCC).** For any structure that is registered, the database includes key information such as: Its exact location (Latitude and Longitude), Its total height above ground and sea level, Ownershiop & Contact Information, Specific instructions for its painting and lighting, history filings, etc. 

The single most important purpose of the ASR program is **aviation safety**. Its goal is to ensure that any antenna structure tall enough to be a potential hazard to aircraft is properly marked (painted) and lit, making it visible to pilots in all conditions. The FCC works with the **Federal Aviation Administration (FAA)** on this[^6]. In simple terms[^7]:

- If a proposed structure is over 200 feet tall or is close to an airport, the owner must first notify the FAA.
- The FAA studies the proposal and, if it's not a hazard, issues a "Determination of No Hazard" that specifies what painting and lighting are required.
- The owner must then take that FAA determination and file it with the FCC to receive an official ASR number, which must be posted at the site.

By the general rule: If you do not have to notify the FAA, you do not have to register with the FCC. Since FCC only has a jurisdiction to antenna structures (could be free standing, built specifically to support antennas, or act as an antenna, or it could be structure mounted on some other man-made object), then any structures (i.e., water towers, buildings, billboards, bridges, windmills, etc.) that do not have an antenna mounted on them are not antenna structures and should not be registered[^8]. 

In Towersource's aspect, we fetch data from the FCC-ASR website which is done at the backend as part of enriching its database. In DQA's perspective, we use the FCC-ASR's [Registraction Search](https://wireless2.fcc.gov/UlsApp/AsrSearch/asrRegistrationSearch.jsp)[^9] tool to search for current ASR registrations that could help in doing research for audit purposes (**"Auditing"** will be discussed further in Section 3 of this document). Shown below are some snippets on what should we expect seeing when one used the said tool: 


![FCC-ASR Registration Search 1](document_images/fcc_asr_ui.png)
![FCC-ASR Registration Search 2](document_images/fcc_asr_ui2.png)
![FCC-ASR Registration Search 3](document_images/fcc_asr_ui3.png)
![FCC-ASR Registration Search 4](document_images/fcc_asr_ui4.png)
![FCC-ASR Registration Search 5](document_images/fcc_asr_ui5.png)

<br>
<br>

## iii. FAA

**FAA Study Number** (also called as Aeronautical Study Number or ASN) is a unique tracking identifier assigned by the Federal Aviation Administration (FAA). Its purpose is to track a specific "Obstruction Evaluation" (OE) case. This process begins when someone (like a developer, tower owner, or crane operator) files a notice (Form 7460-1[^10]) for a proposed structure that is either: Over 200 feet tall, or Close to an airport. 

The FAA then conducts a study using this number to determine if the proposed structure would be a hazard to air navigation. The study concludes with a "Determination" (e.g., "No Hazard," "No Hazard with Lighting," or "Hazard").

A typical study number looks like this: **2025-ASO-12345-OE**. This is a formatted identifier that tells you key information about the case:

- **2025 (Year):** This is the calendar year in which the case was filed.
- **ASO (Service Area / Office):** Three-letter code that identifies the specific FAA regional office or service center that is handling the study. Each region has its own code:

| Code | FAA Service Area / Region   |
|------|-----------------------------|
| AAL  | Alaskan                     |
| ACE  | Central                     |
| AGL  | Great Lakes                 |
| ANE  | New England                 |
| ANM  | Northwest Mountain          |
| ASO  | Southern                    |
| ASW  | Southwest                   |
| AWP  | Western-Pacific             |
| WTW  | Western Terminal Operations |

- **12345 (Sequence Number):** This is a unique sequential number assigned by that specific office for that year.
- **OE (Case Type):** This suffix indicates the type of case. Commonly it is *OE* which stands form *Obstruction Evaluation*.

| Acronym | Case Type              | Definition                                                                                                                                                                                 |
|---------|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OE      | Obstruction Evaluation | This is the most common type. It is a study of a physical structure to see if it  obstructs navigable airspace or interferes with signals.                                                 |
| NRA     | Non-Rulemaking Airport | This study is for proposals on a public-use airport or that affect the airport's layout. Example: A proposal to build a new hangar on an airport's property, or a plan to extend a runway. |
| NR      | Non-Rulemaking         | This is a broader "non-rulemaking" category for aeronautical studies that are  not physical obstructions and not airport layout changes.                                                   |


<br>


Like FCC-ASR, FAA also has an official [Public Search Portal](https://oeaaa.faa.gov/oeaaa/oe3a/main/#/search/records)[^11] for the Obstruction Evaluation / Airport Airspace Analysis (OEAAA) database. The FAA Study Number is the primary key you use on that website to look up the official public record for any given study.

By entering a valid study number into that search page, you can find the structure's details (location, height) and the FAA's final determination, which is the document needed for other permitting, like the FCC ASR. Shown below is an illustration of keying ASN/FAA Study number to pull the filing desired: 

![Keying FAA Study Number 1](document_images/faa_1.png)
![Keying FAA Study Number 2](document_images/faa_2.png)

<br>
<br>

You can also key in by FCC-ASR number to see a historical view of its study numbers as shown below: 


![Keying FCC-ASR 1](document_images/faa_3.png)
![Keying FCC-ASR 2](document_images/faa_4.png)


> an FCC-ASR number can have multiple Study Number associated with it over its lifetime because every time a tower is modified, corrected, or re-evaluated, the FAA treats it as a new "case" and assigns it a new number.


---
# 3. Towersource Proximity Audit Overview

## i. Overview

From the previous section, we talked about Towersource's Data Sources. Now, DQA should perform the "auditing" part to reconcile records in the database coming from these sources regarding which pertains to the same tower and otherwise. Since we capture data from these different sources, it is probabilistic that the same single tower site will show up to these three different sources, one way or the other. 

In the world of Towersource, if a tower asset/record, say, coming from the company pertains to the very same tower showing up from FCC-ASR and/or FAA's website, then the analyst should **"merge"** the records coming from these data sources and create a **singular record** that will capture all of the demographics and technical details of that said tower as complete and accurate as possible. This way, we will not be be overstating the volume of towers we will be committing in our final Towersource database.

But if a **"set of records"** pertain to different towers, then the analyst should not merge any of these records and just to **"Confirm Correct"** that each tower assets/records in the given set are independent and different from each other, and then **"Continue"** to the next set of records to audit. We should not merge any records from a given set of records if these are truly different mounted towers. This way, we will not be understating the volume of towers we will be committing in our final Towersource database.

But what logic should be followed on how to structure these said **"set of records"** that should be grouped together for the analyst to look and do his/her further research? Also, what platform will these audits show up? 

As of the moment, we have the "Sherlock" UI to see all audits that the analyst should research and resolve. Shown below is [Sherlock's UI](https://sherlock.mosaik.com/#/resources/assets)[^12] for Towersource's aspect:


![Glimpse of Sherlock UI](document_images/sherlock1.png)


> The image shown above is a glimpse of what Sherlock UI looks like. This interface is used by the DQA team to retrieve tower assets information and some common translations (i.e., How raw data is being mapped into the standardized and transformed information followed by the legacy Towersource system) from Towersource's database (i.e., Skeletor) without explicity writing SQL code. Additionally, the image shown above is the "Assets" menu of the Towersource aspect of the said UI. Here we can retrieve the demographics and technical information for each tower assets stored in Skeletor. Conjunctionally, we can also select the desired assets here and lay these out in the interactive map shown in the image to visualize the location and whatnot. 

<br>

> But since we're now building the newer platform in Superblocks, with the goal of replacing both Sherlock and Skeletor, these audits will be fully migrated there.

<br>
<br>

In the general world of TowerSource, these audits can be determined through the **"proximity audit"** which is determined under the **"matching"** module of the Towersource system. In the **matching** module, the newly uploaded data, which are coming from the different data sources discussed in the previous section, will be checked against the data that are already committed in the Towersource database. There are various fields used in the matching, like:

- operator_id
- manager_id
- address_id
- type_id
- fcc_asr_number
- faa_study_number
- agl
- amsl
- ground_elevation
- etc.

So say we are trying to load new data in Towersouce. So if the said module will find a perfect match, which means that the new data being loaded finds a perfect match from the data that has already been previously committed in the database, then the older data already committed in the database will be replaced by the newer data being loaded. Some administrative fields like created_at and updated_at will be changed by the timestamp of when the matching have had happened. But if the newer data being loaded will find an ambiguous match with the data that has already been previously committed in the database, which means that some fields are matching but some aren't, then the data that has already been previously committed in the database will not be replaced by the newer data and that the said newer data being loaded will be appended in that same database. Otherwise, if the new data being loaded will not find any matches, then that new data will be considered as a new asset that is not yet known by the Towersource database. 

After all of these matchings ran, then the formation of **"audits"** will now be formed. For simplicity, this formation of audits is a function that will run after the said matchings which will form the **"groups/groupings"** or what we can call as the **"audits"**. This is synonymous to the **"set of records"** that was previously mentioned in this section. These audits follow a certain **"proximity"** or distance in meters of radius within which to limit the extent of assets to look at within the said scope. This proximity is limited to 50m. That's why the geographical data of the tower assets, which are the latitude and longitude, are a must have. So say that if the newly loaded data is a new asset, then his newly loaded data will be the center and it will look around the 50m radius all of the assets that will be within the said scope. For all assets that will be included in the said scope, these assets will now be considered as the **"associated assets"** to the said newly loaded asset. Thus, this newly loaded asset will be then called as the **"focus/reference asset"**. Well, generally, all newly loaded data will be the focus/reference asset of a certain audit or grouping since we need to audit these newly loaded data against the data we already committed in the Towersource database to make sure that we will be reconciling/merging records in the grouping, if needed. Otherwise, no merging is required. It is important to also explicitly mention that an audit or grouping should contain one Focus/Reference record only and at least one Associated record. 

Also since there are instances in the matching where there are ambiguous matches, then those records should be included in the audits and should be looked more by the analyst. These are instances where the newly loaded data appears to have some differences on how it has been loaded previously (e.g., alterations in tower height, changes in coordinates, changes in address, change of ownership, etc.). 

There are more specifics into the formation of the proximity audits. But the ones mentioned in this document are just high level of it. To know more about the formation of audits for Towersource, the reader can visit this [script](https://github.com/teamookla/towersource-data/blob/master/scripts/match.rb) in Towersource GitHub repository[^13]. Note that the scripts there were written using the Ruby programming language. This is one of the key factors on why we will be rebuilding a newer Towersource system; to migrate the legacy Towersource system to a newer platform using Python programming language as its core since this is widely used for general purpose development nowadays and is still robust and smooth for maintenance and improvements down the line.

Now that we know about what a single **audit** or **group/grouping** looks like. We now need to visualize how it looks like by showing some examples. 

<br>
<br>

## ii. Anatomy of Proximity Audit

For this section, we will be visualizing how a single audit or grouping looks like. We will be looking into how it looks like from Sherlock's view. Also, we will be delving into how to pull these audits from the Skeletor database by showing the SQL code for that which will pull all of the important fields used for matching module to have a complete view of each records. 


### a. Proximity Audit from Sherlock's view

Previously, we have introduced a glimpse of Sherlock's UI. To navigate inside the proximity audits that need to be reviewed, one should click the option as shown below: 


![Sherlock Prox Audits 1](document_images/sherlock1_5.png)

<br>

After clicking the Proximity Audit option, it will show you the audits the analyst should research and take further action from that. From the first screenshot shown below, the user can opt to choose what company to look at which is boxed in red. From the first screenshot below, **SBA** company was chosen and these two records showed up. The top row is the focus or reference record/asset. Here, we can see that the focus record was loaded last February 2025 and that the source is the tower company named as SBA. The record below it is the associated record/asset. We can see that the associated record has a user action being committed last February of 2022. This two records forms an audit or grouping. Based on the map, we can see that the two assets are somewhat close with each other, and it should follow the proximity radial distance of 50m from the focus record. We can see also that this grouping showed up in the proximity audit because even though the focus and associated records matched at Tower name, operator site identifier, site status, category, and agl, these records still differ at the operator, manager, and tower type perspective. Also, the focus record don't have an ASR number making the fcc owner name to be blank, while the associated record has an ASR present which enables to lookup for the corresponding fcc owner name. The user can further look into the records one at a time to unpack more information other than what's showing in the screenshot below by clicking the details icon boxed in green (or, the user can right click anywhere in the row and click "Details"). If the user does this, say for the associated record, the second and third screenshot will show up.


![Sherlock Prox Audits 2](document_images/sherlock2.png)
![Sherlock Prox Audits 3](document_images/sherlock3.png)
![Sherlock Prox Audits 4](document_images/sherlock4.png)

<br>

### b. Proximity Audit from Skeletor's view

Evidently, the proximity audits shown by the Sherlock's view is connected from what's available in the Skeletor database. Basically, we can consider the table `towersource.assets` as our fact table while the `towersource.proximity_audit_assets` is one of the dimension tables of Towersource. The `towersource.proximity_audit_assets` designates the grouping, thus it dictates which is the focus asset and which is/are the associated asset/s. This table contains all of the assets that are yet to be audited. Once a grouping or an audit was resolved, that audit or grouping will not show up anymore in this table. To get the important demographics and technical information for both focus and associated records, it is housed by the `towersource.assets`. This table houses all of the assets that have been loaded & audited before, and assets that are yet to be audited. Then there are some of the dimension tables to get the information like asset types, operator name, manager name, tower site address & nation/country, and tower status. 

The complete SQL code to get all of the proximity audits is shown below: 

```sql
WITH x AS
(
SELECT B.focus_asset_id, B.associated_asset_id, A.updated_by AS Source, A.created_at, A.updated_at, ST_Y(A.wkb_geometry) AS Latitude, 
       ST_X(A.wkb_geometry) AS Longitude, A.name AS Name, A.operator_site_identifier AS operator_site_id, C.description AS Type, A.description,
       D.entity_name AS operator_name, A.manager_id, A.agl, A.amsl, A.ground_elevation, A.haat, A.shelter, A.power, A.stories, A.fcc_asr_number, A.faa_study_number,
       A.cdbs_facility_id, A.region, CONCAT(TRIM(E.street1), ' ', TRIM(E.street2), ', ', TRIM(E.city), ', ', TRIM(E.state), ' ', TRIM(E.postal_code), ', ', 
       CASE WHEN TRIM(F.iso_2_abrv) = 'US' THEN 'UNITED STATES' ELSE TRIM(F.iso_2_abrv) END) AS Address, A.construction_date,
       CASE WHEN A.stealth IS NULL THEN 'No' WHEN A.stealth IS FALSE THEN 'No' ELSE 'Yes' END AS stealth, G.name AS asset_status, B.audit_reason
FROM towersource.assets AS A
LEFT JOIN towersource.proximity_audit_assets AS B 
          ON B.associated_asset_id = A.id
LEFT JOIN towersource.asset_types AS C
          ON A.type_id = C.id
LEFT JOIN towersource.operators AS D
          ON A.operator_id = D.id
LEFT JOIN towersource.addresses AS E
          ON A.address_id = E.id
LEFT JOIN towersource.nations AS F 
	      ON E.nation_id = F.id
LEFT JOIN towersource.asset_statuses AS G
          ON A.status_id = G.id
UNION ALL               
SELECT A.id, NULL AS associated_asset_id, A.updated_by AS Source, A.created_at, A.updated_at, ST_Y(A.wkb_geometry) AS Latitude, 
       ST_X(A.wkb_geometry) AS Longitude, A.name AS Name, A.operator_site_identifier AS operator_site_id, C.description AS Type, A.description, 
       D.entity_name AS operator_name, A.manager_id, A.agl, A.amsl, A.ground_elevation, A.haat, A.shelter, A.power, A.stories,  A.fcc_asr_number,
       A.faa_study_number, A.cdbs_facility_id, A.region, CONCAT(TRIM(E.street1), ' ', TRIM(E.street2), ', ', TRIM(E.city), ', ', TRIM(E.state), ' ', TRIM(E.postal_code), ', ', 
       CASE WHEN TRIM(F.iso_2_abrv) = 'US' THEN 'UNITED STATES' ELSE TRIM(F.iso_2_abrv) END) AS Address, A.construction_date,
       CASE WHEN A.stealth IS NULL THEN 'No' WHEN A.stealth IS FALSE THEN 'No' ELSE 'Yes' END AS stealth, G.name AS asset_status, 'Focus Asset' AS audit_reason
FROM towersource.assets AS A
LEFT JOIN towersource.proximity_audit_assets AS B 
          ON B.associated_asset_id = A.id
LEFT JOIN towersource.asset_types AS C
          ON A.type_id = C.id
LEFT JOIN towersource.operators AS D
          ON A.operator_id = D.id
LEFT JOIN towersource.addresses AS E
          ON A.address_id = E.id
LEFT JOIN towersource.nations AS F 
	      ON E.nation_id = F.id
LEFT JOIN towersource.asset_statuses AS G
          ON A.status_id = G.id
WHERE A.id IN (SELECT DISTINCT focus_asset_id FROM towersource.proximity_audit_assets)
), 
y AS 
(
SELECT x.focus_asset_id, z.updated_by AS focus_asset, x.associated_asset_id, x.source, x.created_at, x.updated_at, x.latitude, x.longitude, x.name, 
       x.operator_site_id, x.type, x.description, x.operator_name, j.entity_name AS manager_name, i.entity_name AS fcc_owner_name, x.agl, x.amsl, x.ground_elevation,
       x.haat, x.shelter, x.power, x.stories, x.fcc_asr_number, x.faa_study_number, x.cdbs_facility_id, x.region, x.address, x.construction_date, x.stealth,
       x.asset_status, x.audit_reason
FROM x 
LEFT JOIN towersource.assets AS z
		  ON x.focus_asset_id = z.id
LEFT JOIN towersource.operators AS j
          ON x.manager_id = j.id
LEFT JOIN towersource.asr_company_map_bak AS i
          ON x.fcc_asr_number =  i.fcc_asr_number
)
SELECT DISTINCT y.focus_asset_id, y.focus_asset, y.associated_asset_id, y.source, y.created_at, y.updated_at, y.latitude, y.longitude, y.name, 
       y.operator_site_id, y.type, y.description, y.operator_name, y.manager_name, y.fcc_owner_name, y.agl, y.amsl, y.ground_elevation, y.haat, 
       y.shelter, y.power, y.stories, y.fcc_asr_number, y.faa_study_number, y.cdbs_facility_id, y.region, y.address, y.construction_date, 
       y.stealth, y.asset_status, y.audit_reason
FROM y
WHERE y.focus_asset_id IS NOT NULL          
ORDER BY y.focus_asset_id, y.associated_asset_id NULLS FIRST;
```

<br>

Shown below is one example of an audit or grouping. In the said query output, if the records have the same  `focus_asset_id`, then those records corresponds to an audit or grouping. In an audit/grouping, the record with `NULL` `associated_asset_id` is the focus record, while the records with `NOT NULL` `associated_asset_id` are the associated records: 


| focus_asset_id | focus_asset                     | associated_asset_id | source                          | created_at          | updated_at          | latitude | longitude  | name             | operator_site_id | type                    | description | operator_name                   | manager_name | fcc_owner_name                     | agl  | amsl  | ground_elevation | haat | shelter | power | stories | fcc_asr_number | faa_study_number | cdbs_facility_id | region | address                                                  | construction_date | stealth | asset_status | audit_reason          |
| -------------- | ------------------------------- | ------------------- | ------------------------------- | ------------------- | ------------------- | -------- | ---------- | ---------------- | ---------------- | ----------------------- | ----------- | ------------------------------- | ------------ | ---------------------------------- | ---- | ----- | ---------------- | ---- | ------- | ----- | ------- | -------------- | ---------------- | ---------------- | ------ | -------------------------------------------------------- | ----------------- | ------- | ------------ | --------------------- |
| 1147142        | Everest Infrastructure Partners |                     | Everest Infrastructure Partners | 2025-02-18 16:27:16 | 2025-02-18 16:27:16 | 46.68272 | \-67.99925 | 333 State St     | US645557         | Lattice / Self Standing |             | Everest Infrastructure Partners |              | Spectrum Northeast, LLC            | 6.4  | 209.1 | 202.7            |      |         |       |         | 1304467        | 2017-ANE-3794-OE |                  |        | 333 State St , Presque Isle, ME 04769, UNITED STATES     |                   | No      | Dismantled   | Focus Asset           |
| 1147142        | Everest Infrastructure Partners | 820988              | sgaither                        | 2015-04-21 18:15:04 | 2023-01-09 16:50:37 | 46.68269 | \-67.99869 | Presque Isle     |                  | Lattice / Self Standing | LTOWER      | Charter Communications          | KGI Wireless | Spectrum Northeast, LLC            | 9.1  | 215.5 | 206.4            |      |         |       |         | 1304467        | 2017-ANE-3794-OE |                  |        | 329 State St , Presque Isle, ME 04769, UNITED STATES     | 1981-06-01        | No      | Dismantled   | Proximity Audit (42m) |
| 1147142        | Everest Infrastructure Partners | 963158              | ASR                             | 2019-10-16 10:34:55 | 2019-10-16 10:34:55 | 46.68269 | \-67.99925 | 331 State Street |                  | Monopole                | MTOWER      | AT&T                            |              | Northeast Wireless Networks, LLC   | 30.5 | 234   | 203.5            |      |         |       |         | 1295433        | 2019-ANE-2510-OE |                  |        | 331 State Street , Pesque Isle, ME 04769, UNITED STATES  | 2015-04-10        | No      | Active       | Proximity Audit (3m)  |
| 1147142        | Everest Infrastructure Partners | 1048858             | sgaither                        | 2015-02-03 23:55:20 | 2023-01-06 22:58:37 | 46.68268 | \-67.9992  | Presque Isle Dt  | 444389           | Monopole                | POLE        | USCellular                      |              | UNITED STATES CELLULAR CORPORATION | 30.4 | 234.6 | 204.2            |      |         |       |         | 1240747        | 2023-ANE-3329-OE |                  |        | 280 State Street , Presque Isle, ME 04769, UNITED STATES | 2015-03-24        | No      | Active       | Proximity Audit (5m)  |

<br>

The output of this query will be fed to the auto-merging process. For the next sections, we will now be delving into the said designed process from a surface level down to the most granular level. 
<br>

---
# 4. Auto-Merging's Designed Process Overview

From the previous sections, we have motivated and defined important aspects of Towersource that should serve as an overview or refresher of the things that the reader should know and be familiarized before delving into the auto-merging process itself. We're at this point in the document to introduce the meats-and-potatoes of what should be expected for the **auto-merging process**. 

As we load more company tower sheets into the Towersource database, it will also directly affect the volume of audits that will be formed. This will create a lot of weight, specifically to the analyst's standpoint, because this will also require a lot of research and auditing that needs to be done before we finally commit these newly loaded data into the assets' database. But it is a given fact also that not all of these audits or groupings require in depth approach in terms of doing research and whatnot. Some of the groupings exhibit an evident behaviour wherein a reconciliation or merging of the focus and associated assets can be done without doing a lot of footwork and investigations.

This is where the motivation to create an automated process comes into play. This part of the project has the goal to perform an automated merging based on the specific sets of criteria that should be met. These specific sets of criteria were carefully designed from the rigorous reviews that the team have performed specifically though the commonalities that can be seen in production where merging should take place. The main challenge into the curation of this process is "how are we going to create an automated process that can distinguish if the records from a given audit or grouping pertains to the same tower?". The common answer for this is to use parameters that can innately identify one tower from another. The main proponents considered in this process to make the automation accurately distinguish which records pertain to the same tower are the tower identifiers discussed in the previous sections -- **FCC-ASR Number** and the **FAA Study Number**. From these two parameters, we have created a starting point on how we will be designing the sets of criteria. This point is where we have created five commonly seen cases where auto merging could happen. These cases are highly dependent on the presence and combination of FCC-ASR and FAA Study Number: 


### **Case 1**
Both the Focus/Reference record and the Associated Record/s have the same NON NULL FCC-ASR Number and FAA Study Number.

<br>

### **Case 2** 
Both the Focus/Reference record and the Associated Record/s have the same NON NULL FCC-ASR Number but have different NON NULL FAA Study Number.

<br>

### **Case 3**
Both the Focus/Reference record and the Associated Record/s have the same NON NULL FCC-ASR Number but either the Focus/Reference record or the Associated Record/s have NULL FAA Study Number.

<br>

### **Case 4**
The Focus/Reference record have NULL FCC-ASR Number and FAA Study Number while the Associated Record/s have NON NULL FCC-ASR Number and FAA Study Number.

<br>

### **Case 5**
Both Focus/Reference record and Associated Record/s have NULL FCC-ASR Number and FAA Study Number.

<br>

Based from each of these Five Cases, the merging candidates were pulled from the database. And then from these merging candidates for each cases, the sets of criteria were carefully designed so that auto merging of records that shouldn't be merged would be prevented. 

These Cases will run Chronologically - Case 1 will run first and then Case 5 will run the last - and the result of the previous case will be fed to the next case. To further visualize this - Treat these cases as "Sieve" that are vertically stacked, where Case 1 is at the top while Case 5 is at the bottom. As we go down the level of Sieve, the mesh size gets smaller. This means that the level of restriction and complexity in terms of the conditions will be higher as we go down each sieve. Thus, say, all particles that will be successfully strained by Case 1's Sieve will be the fed particles for Case 2's Sieve, and so on. Thus, all particles that will not be strained by each Case's Sieve will be the ones that should be auto-merged.

For the next section, we will be delving into the surface level logic that should be followed by each of the five cases. For brevity, these surface level logic is patterned such that each of the cases are uniformly designed to be the same. But, the sub logics for each of the cases will be somewhat unique from each other since each cases have different combination of the said primary identifiers. One should expect that as we go higher in terms of Case number that the sub logics will be more restrictive to prevent inaccurate auto merging to happen.

---
# 5. Auto-Merging's High Level Logic

In the previous section, it was mentioned that the surface level logic for each of the five cases are patterned such that all will be uniformly designed to be the same. In this section, we will be exploring these surface level logic and what high level logic should run for each. 

For the auto-merging process, we have three main chunks of logic that are followed for each of the five cases. In chronological order, these chunks are:

### **i. Merging Candidates Conditions** 

This is the first chunk of logic that will kick-off for the auto-merging process. The goal of this logic is to iterate for each of the grouping to find instances where the certain-defined fields from the focus/reference record are matching with the associated record/s. If the grouping's focus/reference record won't find any associated record that will match at these certain-defined fields, then the whole grouping won't have any successful auto merging. Otherwise, these matching records will be considered as candidates for auto-merging and will proceed with the next consecutive chunks of logic.

As one can notice, we can say that Case 1 has the most confidence level in terms of matching an associated record to its corresponding focus/reference record in a given grouping that gives the assurance that these pertains to the same tower asset. Reason behind is that both focus/reference and associated record share the same primary identifiers for a tower asset (i.e., FCC-ASR Number and FAA Study Number). Thus, the level of restriction in terms of matching and whatnot is not that restrictive for this case. Thus, one can also notice at this point that as we go down each cases, the level of restriction will go higher since the confidence level in terms of matching gets lower due to some differences or missing element/s from our primary identifiers between the focus/reference record and the corresponding associated record/s. This will create more complexity in the logic as we go down each cases. 

In section 7, we will be exploring the algorithm for Merging Candidates rigorously and how the sub logic is changing for each cases.

<br>
<br>

### **ii. Further Filter & Merging Conditions**

After the Merging Candidates Conditions ran, the Further Filter Conditions will kick-off. Not all of the records that were found to be merging candidates in a given grouping can be auto-merged immediately even though they matched at certain-defined fields. From the commonalities review done prior to the design of auto-merging process, we saw cases wherein multiple towers are present in a certain proximity that shares the same, say, study number and/or operator site identifier and/or site name and/or operator, etc. This is why the Further Filter was created; to add an extra-added layer of safeguard to make sure that the records that we will be auto-merging are truly pertaining to the same tower. Thus, Further Filter Conditions can be considered as a helper function for us to make sure that the records we will be auto merging are accurate and to remove records that should not be included in the auto-merging process. Same as with Merging Candidates Conditions, the Further Filter Conditions will be more complex as we move along each of the cases.

After the Further Filter Conditions, then the Merging Conditions will now kick-off. Since we already filtered the merging candidates to get which should be auto-merged, now is the time to merge these successful records from a given grouping. For the Merging Conditions, Cases 1 through 5 should just be the same. 

In Section 7, we will be exploring the algorithm for both Further Filter and Merging Conditions rigorously and how the sub logic is changing for each cases.

<br>
<br>

### **iii. Maintenance Conditions**

After the Further Filter & Merging Conditions ran, the Maintenance Conditions will kick-off. Basically, this chunk will just perform some cleanups and preparations for the total and finalized output of each case. This way, the said process is preparing the updated list of groupings that needs to be further investigated by the next consecutive cases. 

Again in Section 7, we will be exploring the algorithm for the Maintenance Conditions.  

---
# 8. Future Plans

The team is expecting to add more Cases for the auto-merging process as we see more examples and as we load more company tower sheets. In fact, Case 6 is currently being studied that was motivated from Capital Telecom's way of reporting their data to us. The team is further looking into this possibility of adding Case 6 and the chances that it can affect other tower companies as well, not just Capital telecom. Thus in the future, it is expected that we will have a growing number of Case X for the auto-merging process.

Also, a possible deduplication process is being looked at for the auto-merging process. We are seing some instances where multiple records just pertain to the same tower. But since each of these multiple records has their own grouping, these were treated independently. Thus in the future, we will be curating a deduplication process which will trigger after all Cases ran, so that we will not be overstating tower assets. Even though this will only affect a small portion of the Towersource Database, it is still better to keep this aspect under our radar. 

Regarding the Standard Operating Procedure that should be followed by the DQA team with the addition of this automated process, the results produced by the auto-merging process should also be looked at to make sure that the said process is auto-merging records in a certain grouping accurately. The possibility of creating a dashboard or a simple report showing these results is being planned. This new SOP might or might not be in perpetuity, but the team is planning on how this will be handled in short and long term approach.


---
# 9. References

[^1]: Ookla's [Towersource](https://www.towersource.com/) User Interface
[^2]: Documentation for [Superblocks](https://docs.superblocks.com/)
[^3]: Python Library Package Documentation for [requests](https://requests.readthedocs.io/en/latest/)
[^4]: Python Library Package Documentation for [Selenium](https://selenium-python.readthedocs.io/)
[^5]: Python Library Package Documentation for [BeautifulSoup](https://pypi.org/project/beautifulsoup4/)
[^6]: Code of Federal Regulations, Title 47, Part 17.4 – "Antenna structure registration." [https://www.ecfr.gov/current/title-47/chapter-I/subchapter-A/part-17/subpart-A/section-17.4](https://www.ecfr.gov/current/title-47/chapter-I/subchapter-A/part-17/subpart-A/section-17.4)
[^7]: Code of Federal Regulations, Title 14, Part 77.9 – "Construction or alteration requiring notice." [https://www.ecfr.gov/current/title-14/chapter-I/subchapter-E/part-77/subpart-B/section-77.9](https://www.ecfr.gov/current/title-14/chapter-I/subchapter-E/part-77/subpart-B/section-77.9)
[^8]: FCC Antenna Structure Registration (ASR) - Overview. [https://www.fcc.gov/wireless/support/knowledge-base/antenna-structure-registration-asr-resources/antenna-structure](https://www.fcc.gov/wireless/support/knowledge-base/antenna-structure-registration-asr-resources/antenna-structure)
[^9]: FCC-ASR Registration Search tool. [https://wireless2.fcc.gov/UlsApp/AsrSearch/asrRegistrationSearch.jsp](https://wireless2.fcc.gov/UlsApp/AsrSearch/asrRegistrationSearch.jsp)
[^10]: FAA Form 7460-1 - "Notice of Proposed Construction or Alteration". [https://www.faa.gov/documentlibrary/media/form/faa7460_1.pdf](https://www.faa.gov/documentlibrary/media/form/faa7460_1.pdf)
[^11]: FAA's official public search portal for the Obstruction Evaluation / Airport Airspace Analysis (OEAAA) database.. [https://oeaaa.faa.gov/oeaaa/oe3a/main/#/search/records](https://oeaaa.faa.gov/oeaaa/oe3a/main/#/search/records)
[^12]: Towersource aspect in Sherlock's UI that shows the "assets" information currently stored in Towersource database (i.e., Skeletor). [https://sherlock.mosaik.com/#/resources/assets](https://sherlock.mosaik.com/#/resources/assets)
[^13]: Towersource GitHub repository. [https://github.com/teamookla/towersource-data/tree/master](https://github.com/teamookla/towersource-data/tree/master)
