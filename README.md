# Title Express Data Tidying

A notebook of R scripts to extract, prepare, and combine data from SMS Title Express and First American Title's "Agent Net" for easy analysis. 

Requires R and RStudio to run, plus the following packages installed:
* tidyverse
* readxl
* lubridate
* knitr

Includes light interactive elements to choose select the file-paths for each sheet of data exported from Title Express and AgentNet. 




Before running the script in the notebook, you'll need to gather a few sets of data:
* three exported searches from the "Find" tab of Title Express' main menu, 
* an exported Sales Utility report from Title Express' "Reports" function,  
* a list of computed balance book transactions from Title Express' "Escrow Accounting" function, 
* a Policy Log Report from First American's AgentNet website

Before you get started, you also need to decide on the range of open dates for the files you want to view. 

Here's how to retrieve and save each of them: 

## Exporting Data From the "Find" Tab:

* use the drop-down menus under *Search for Orders* to select "Open Date", and the start-and end dates for the range you've chosen. 
* use the drop-down menu under *View* to select "Dates", then click *Search*
* click *Export Results*, enter a name for the .csv file of your search results (something like "dates data"), and save it somewhere you can easily find it. 
* repeat the previous steps twice, selecting "Address" and "Loan" each time and giving each new file an approproate name. 


## Exporting Data From the "Reports" Function:

* click *Reports* in the sidebar of Title Express' main menu
* click *Management* in the new popup
* use the drop-down menu next to *Type* to select "History", and the menu next to *Report* to select "Sales Utility - Client"
* under the options that appears:
	+ select all available order statuses
	+ select your chosen open dates for *Date Range*, and "Open Date" for *Date Source*
	+ select "Transaction Amounts" for *Report Style*
* after a new window with the report results pops up, click the Export icon near the top of the window, next to the Printer icon
* enter an appropriate name (like "transaction amounts"), choose the ".xlsx" option for the file type, and save it in the same location as the previous files. 


## Exporting Data From the "Escrow" Function:

Getting this data requires a little preparation on your end. 

First, you need to export the raw data: 
* click *Escrow Accounting* in the sidebar of Title Express' main menu
* click *Reports* in the new popup
* choose "Research" for *Type* and "Computed Book Balance Transactions" for *Report*
* in the *Options* section, 
	+ click the button next to "By Dates"
	+ choose "File Number" for *Sort By*
	+ for *Prior Period Ending Date* enter the day before your range of open dates 
	+ for *Current Period Ending Date* enter a date about 90 days after the end of your range of open dates (this makes sure that you capture all transactions associated with each case)
* click "Prepare Report", then click the Export icon, give the new file an approproate name, choose the ".xlsx" option for the file type, and save it in the same location as the previous files.

Now you need to do about one minute to prepare the date you've just exported. 

If you up the file you've just created and scroll down, you'll see that the Deposit transactions are listed in the top half of the spreadsheet and the Disbursement transactions are listed in the bottom half of the spreadsheet, with a few empty rows and a new header between them. Here's how to get this data ready for R to read:
* insert a new column on the far left side of the spreadsheet (new Column A), and name it "Category" (leave out the quotation marks when you type it into excel). 
* fill each row of your new column with "Deposit" or "Disbursement" for each set of transactions
* delete the rows below each section summarizing deposits and disbursements
* delete the empty rows between "Deposit" and "Disbursement" sections
* delete the extra set of column-headers before the "Disbursement" section
* delete all rows between the metadata/header and first row of column headings (data should start of 7th row)
* delete the rows of information after the last "Disbursement" transaction in the spreadsheet
* save your work and close the file!


## Exporting a Policy Log First American Title's "AgentNet" website

* log into your Agent Net Homepage, hover over "My AgentNet" and click "My Reports"
* next to *Report Name*, select "Policy Log" and then select "Excel" for your format
* next to *Date*, select "Date of Policy"
* for *Date Range*, use same start-date of your Open Date Range that you've used for your other data exports, and enter a date about 90 days after the end of your range of open dates. 
* click "Submit", enter your email in the pop-up, and wait a few minutes for the file to be delivered. 

Save the new file on your computer, and you're ready begin analysing the files in R!