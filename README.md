# batchlauf

## Technical

* Use environment variables for database connection details: `const MYSQL_HOST = process.env.MYSQL_HOST || "localhost";`
* Invoice Data Mapping: [https://docs.google.com/spreadsheets/d/1TPkIlSR_OsiLF-s1m5lYEvDTVJrb25OculZYXwEstnA/edit?usp=sharing](Google Spreadsheet)


## Assignment Overview

The goal is to create a Webapp - invoice_generator (SPA) that imports datasets for invoices from a MySQL DB. 

The user shall then control via Front end the invoice generation process. Finally must the Webapp produce invoices according to the provided template, which can be reviewed in the webapp on specific browsers (Chromium, Firefox) and converted into a PDF file.

## Details of the assignment
### 1. General Structure
- Print a 4-page pdf with chromium browser in headless mode
- Webapp to run in a Browser: 
  - chromium browser (open source part of google chrome) >= version 61	
    - Firefox >= version 54
- the entire Webapp is hosted on AWS 
  - EC2 
  - RDS
  - S3 
- the solution will be completely dockerized, meaning we will run the website later inside our docker swarm mode
- the docker swarm - worker process (which is generating the pdf) is a seperate service that we can scale in our docker swarm mode docker service scale super_pdf_service=15
- this service `queue_data_provider` is only accessable within our docker swarm network
- When opening without arguments you should see a plain invoice representing the invoice design where you can enter data in the respective fields
- Invoice processing/ generation must be possible as batch run, letting the user select a set of datasets from the attached MySQL DB to be converted into invoices
- Selection is supposed to be done by 
  - invoice month (like december invoices)
  - Contract number
  - date
- one should be able to edit the entered/ imported data 
  - when hitting `ctrl + shift + o`, a textbox should appear where we can paste a single json string, click `OK`, and the pasted data should be used for the invoice generation (manual debugging and editing of invoices)
  - the resulting data must be recorded in the MySQL Database accordingly
- table rows on the invoice template must only be generated as many as needed in the invoice
- we need to store one converted pdf file
- Include Swagger for API documentation


### 2. References
- Invoice template: https://marvelapp.com/4b419jd
- our vacation request form: http://markuman.gitlab.io/urlaubsantrag/
- Invoice generator technology example: https://invoice-generator.com/#/1
- Invoice plane: https://github.com/InvoicePlane/InvoicePlane

### 3. Technology Stack
- HTML5
- CSS3 (no preprocessor)
- CSS Grid/Flexbox
- Vuejs/ Javascript 
- use `fetch()` api, not jquery or xhr!
- Docker Swarm Mode
- included in alpine:3.7 base image
- busybox can ship the index.html, no addition webserver needed: `ENTRYPOINT busybox httpd -p 80 -h /app && tail -f /dev/null`
- MySQL / RDS
- AWS S3
- Swagger

### 4. provided by us
- a psd file as letter template
- invoice as CSS3/ HTML5

### 5. Timeline

- the timeframe for the project is set to 3 weeks upon hiring the developer 
- meaning the invoice generator must be ready to deploy 02.02.17



## PRODUCTION

1. `make all`
  - this should build all docker images for the needed services
2. `docker stack deploy -c invoice_service.yml invoice`
  - everything should be deployed with one command

## Milestones
| #    | Description                              | Delivery Date |
| ---- | ---------------------------------------- | ------------- |
| 1    | create Swagger API                       | 17.01         |
| 2    | dev API/ backend                         | 22.01         |
| 3    | finish docker images for backend         | 22.01         |
| 4    | first draft front end design web app invoice generator | 24.01         |
| 5    | review the design with content and make final decision after changes | 25.01         |
| 6    | finish front end design web app invoice generator | 26.01 |
| 7    | finish docker image frontend and hosting on AWS | 26.01         |
| 8    | front end / backend integration on AWS; docker swarm | 29.01         |
| 9    | final tests                              | 30.01.        |
