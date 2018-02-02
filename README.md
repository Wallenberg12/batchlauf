# batchlauf

## Technical

* Use environment variables for database connection details: `const MYSQL_HOST = process.env.MYSQL_HOST || "localhost";`
* Invoice Data Mapping: [https://docs.google.com/spreadsheets/d/1TPkIlSR_OsiLF-s1m5lYEvDTVJrb25OculZYXwEstnA/edit?usp=sharing](Google Spreadsheet)


## Assignment Overview

The goal is to create a Webapp - invoice_generator (SPA) that imports datasets for invoices from a MySQL DB. 

The user shall then control via Front end the invoice generation process. Finally must the Webapp produce invoices according to the provided template, which can be reviewed in the webapp on specific browsers (Chromium, Firefox) and converted into a PDF file.

## Details of the assignment
