# ClimbingProject

##Process Outline:

- Load data from static CSV files into Azure Data Lake Gen2

- Use Azure Data Factory to move CSV data into a Azure SQL Database

- Use Power BI to analyse data in Azure SQL Database


Let start at the Azure portal home page:  https://portal.azure.com/

#1. Create Resource Group

We need to create a resource group to have all the Azure products in one place.

Select the Resource Groups icon 

![Resource Groups](https://user-images.githubusercontent.com/61860904/107544144-262a5e80-6b87-11eb-9eed-ad42ff619ae8.PNG)

Then create one.

![Create Resource Group](https://user-images.githubusercontent.com/61860904/107544611-a5b82d80-6b87-11eb-8c03-6333e8a7c414.PNG)

Select your subscripton and give the Resource Group a name, then choose the region closest to you.

Review+Create your Resource Group




#2. Load Data into Azure Data Lake Gen2 



We need to create the Data Lake for our CSV's to live in. There are two places to ceate a new resource from the home page as shown below:

![Create Resource](https://user-images.githubusercontent.com/61860904/107542861-deef9e00-6b85-11eb-9b77-93ae106fb22c.PNG)

Or you can select "Add" within your Resource Group

![Add Resource](https://user-images.githubusercontent.com/61860904/107545846-f8deb000-6b88-11eb-869b-a308583975d9.PNG)

Search for "Storage Account".

![Storage Account](https://user-images.githubusercontent.com/61860904/107543424-75bc5a80-6b86-11eb-8f89-8222b86d9316.PNG)

Press "Create"

![Create Storage Account](https://user-images.githubusercontent.com/61860904/107543644-a3090880-6b86-11eb-8a1d-35e8a8e58eee.PNG)

Choose your Subscription and Resource Group.

Name your storage account and choose the same location chosen for the Resource Group.

Go to the "Advanced" tab and select Data Lake Storage Gen2. 

![Advanced - Data Lake](https://user-images.githubusercontent.com/61860904/107546594-c5e8ec00-6b89-11eb-87c3-a78f8dd7271f.PNG)









