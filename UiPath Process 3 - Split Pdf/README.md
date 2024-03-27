# UiPath Process 4 - Split PDF

## Workflow seems to be aimed at splitting a PDF file based on changes in invoice numbers, with each section separated into individual PDFs. The process involves reading the PDF, extracting text, finding invoice numbers, and then splitting the PDF accordingly.

## Variable Initialization: 
The workflow initializes several variables including intIndex, FilePath, intTotalNumberOfPages, strPdfText, strTemp, and intPageCounter.

## Assign File Path: 
The file path of the PDF file to be processed is assigned to the FilePath variable.

## Get PDF Page Count: 
The total number of pages in the PDF file is retrieved and stored in the intTotalNumberOfPages variable.

## Log Number of Pages: 
The total number of pages in the PDF is logged for reference.

## Loop Through PDF Pages: 
The workflow enters a loop (InterruptibleWhile) that iterates through each page of the PDF until a certain condition is met. The loop condition is [intIndex <= intTotalNumberOfPages], meaning the loop continues as long as the intIndex is less than or equal to the total number of pages.

## Read PDF Text: 
For each iteration of the loop, the text from the current page of the PDF (indicated by intIndex) is read and stored in the strPdfText variable.

## Find Invoice Number: 
The workflow uses a regular expression pattern (\d{12}) to find the invoice number within the text of the current page. The matched invoice number is stored in the strInvoiceNumber variable.

## Check for Change in Invoice Number: 
The workflow checks if the current invoice number (strInvoiceNumber) is different from the previous one (strTemp). If it's the same or if strTemp is empty, it executes the "Then" sequence. Otherwise, it executes the "Else" sequence.

## Then Sequence (Same Invoice Number):
The current invoice number is assigned to strTemp.
The intPageCounter is incremented by 1.
A log message is generated indicating the page, invoice number, and page counter.

## Else Sequence (New Invoice Number):
The current invoice number is assigned to strTemp.
A log message is generated to indicate a break point.
A range of pages from the previous invoice to the current page is extracted and saved as a separate PDF file.
The intPageCounter is reset to 1.

## Increment Page Index: 
The intIndex is incremented by 1 to move to the next page of the PDF.

## Loop Continues: 
The loop continues until all pages of the PDF have been processed.