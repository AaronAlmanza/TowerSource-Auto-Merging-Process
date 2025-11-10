<hr style="border: 3px solid Cyan;">

# Table of Contents

<hr style="border: 1px;">

1. Introduction
<!--- Here I'll explain what this document is all about, which is all about auto-merging, and how it will help the future analysts to focus more on prox audits that require more in depth research. I need to create the motivation on what to expect in this document and how we will be slowly curating some theoretical and technical aspects that the reader should know before he/she can understand the fundamentals of auto-merging process itself, like: We'll tackle the primary identifiers used to determine information about towers (FAA and FCC) and show what they signify and where we can get those information (maybe we can google search some of the definition of terms and crash courses about these), talk about the proximity audits in Sherlock's perspective, talk about the proximity audits in Skeletor's perspective, talk about the anatomy of a group or single prox audit, talk about how prox audits can be queried from the backend tables, talk about auto-merging and how it will help us in implementing automation jobs, --->
2. TowerSource's Data Source Overview
   1. Company data
      <!---a.) Outreach (Show an example of email sent to the companies and the example raw tower sheet we received from them, also say that not all companies are reporting complete data), b.) Web Scraping (Show websites where they have site locators in a form of maps or something where web scraping can be performed)--->
   2. FCC-ASR
      <!-- Show the website, link the website, describe what the website is all about, show an example of a complete tower information. --->
   3. FAA
      <!-- Show the website, link the website, describe what the website is all about, show an example of a complete tower information. --->
      
3. Sherlock's Proximity Audit Overview
   1. Overview
      <!-- From the previous section, we talked about the Tower Assets' sources. Now, the Data Analysts should now perform some auditing to reconcile records in the database coming from these sources regarding which pertains to the same tower and otherwise. Since we capture data from these different sources, it is probabilistic to think that a single tower site will show up to these three different sources, one way or another. In the world of Towersource, if a tower asset/record, say, coming from the company pertains to the same tower showing from FCC-ASR and/or FAA's website, then the analyst should "merge" the records and create a singular record that will capture all of the demographics and techinical details of that said tower as complete and accurate as possible. But if a set of records pertain to different towers, then the analyst should not merge any of these records and just to "Confirm Correct" that each records are independent and different from each other, and then "Continue" to the next set of records to audit. But what logic should be followed on how to structure these "set of records" that should be grouped together for the analyst to look and do his/her further research? Also, what platform will these audits show up? As of the moment, we have the "Sherlock" UI to see all audits that the analyst should research and resolve (Show Sherlock), but since we're building the newer platform now in Superblocks these audits will be migrated there. In the general world of TowerSource, these audits can be determined through the "proximity audit". Here, I should define Proximity audits and the basic overview logic behind it. I should make it a point that it is very important to have the geographical coordinates shown by a specific tower site coming from either the Company', FCC-ASR's or FAA's website to determine which of the records should be grouped together and be further analyzed by the analyst simultaneously. A single "grouped" records based on proximity audit's logic can be called as a single "audit" or "group/grouping". As we load newer tower information coming from these different sources,  But what are the parts of a single "audit" or "grouping"?---> 
   2. Anatomy of Proximity Audit
      1. Proximity Audit from Sherlock's view
         <!-- Just show an example proximity audit and point out which is the reference/focus record and which is/are the associated record/s. --->
      2. Proximity Audit from Skeletor's view
         <!-- What table should give you the information about which if the focus and which are the respective associated records? What table should be used to join this proximity audits table to determine a more in depth tower information for each. Show here and link the SQL I wrote to get these information. Put a disclaimer that we will not be using delving into the "dimensions" table (i.e., manager_table, operator_table, etc.). We will end this section by showing the whole SQL and the snippet of the output (without the AGL thingies yet). --->
         
4. Auto-Merging's Designed Process Overview
 <!--- Here, I will just introduce again the auto-merging process and the goal of creating an automated process for the merging process so that the analyst will only focus more on "audits" or "groupings" where further human intervention is required (i.e., further research, further traversing of the maps, further inquiries, etc.). I will discuss here that we will be using as a 'primary identifier' the FCC-ASR and FAA study number to determine one tower from another. These two ingredients will help us determine which focus/reference record should be merged to their respective associated record, and which shouldn't be merged and just do nothing with the records in a grouping or audit. And then from these identifiers, we can create different combination scenarios for FCC-ASR or FAA on how these two ingredients would show up in a grouping or audit. We will call these combination of scenarios as "cases". For the first implementation of the auto-merging process, we devised the 5 major cases: blablablabla -->  

5. Auto-Merging's High Level Logic
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
      
8. Future Plans
   <!--- In the future, we are to expect that we will be seeing more opportunities to expand the functionality of the auto-merging process from the five major cases we focused on. As of now, we are studying the possibility of having Case 6 (and then just give an overview on how it looks like and an example). --->

10. Bibliography
     <!---I can create a numbering style (like in RRL) for each parts in the main documentation and then cited in this chapter. --->
     <!---FCC-ASR Website, research papers where FCC-ASR has been released or reviewed, FAA's website, research papers where FAA has been released or reviewed, packages used in Python (each packages should be cited using their documentation (can be a URL) --->

<hr style="border: 3px solid Cyan;">
