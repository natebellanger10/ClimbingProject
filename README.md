# ClimbingProject

## Process Outline:
1. Create Resource Group 
2. Create Azure Data Lake Gen2
3. Load data from on premises into Azure Data Lake
4. Create Azure SQL Database
5. Use Azure Data Factory to move data
6. Use Power BI to analyse data in Azure SQL Database


<br/>
<br/>
Lets start at the Azure portal home page:  https://portal.azure.com/
<br/>
<br/>

## 1. Create Resource Group

- We need to create a resource group to have all the Azure products in one place for our project.

- Select the Resource Groups icon: 

<kbd> ![Resource Groups](https://user-images.githubusercontent.com/61860904/107544144-262a5e80-6b87-11eb-9eed-ad42ff619ae8.PNG) </kbd>

- Then create one.

<kbd> ![Create Resource Group](https://user-images.githubusercontent.com/61860904/107544611-a5b82d80-6b87-11eb-8c03-6333e8a7c414.PNG) </kbd>

- Select your subscripton and give the Resource Group a name, then choose the region closest to you.

- Review+Create your Resource Group

<br/>
<br/>

## 2. Create Azure Data Lake Gen2

- We need to create the Data Lake for our CSV's to live in. There are two places to ceate a new resource from the home page as shown below:

<kbd> ![Create Resource](https://user-images.githubusercontent.com/61860904/107542861-deef9e00-6b85-11eb-9b77-93ae106fb22c.PNG) </kbd>

- Or you can select "Add" within your Resource Group

<kbd> ![Add Resource](https://user-images.githubusercontent.com/61860904/107545846-f8deb000-6b88-11eb-869b-a308583975d9.PNG) </kbd>

- Search for "Storage Account".

<kbd> ![Storage Account](https://user-images.githubusercontent.com/61860904/107543424-75bc5a80-6b86-11eb-8f89-8222b86d9316.PNG) </kbd>

- Press "Create"

<kbd> ![Create Storage Account](https://user-images.githubusercontent.com/61860904/107543644-a3090880-6b86-11eb-8a1d-35e8a8e58eee.PNG) </kbd>

- Choose your Subscription and Resource Group.

- Name your storage account and choose the same location chosen for the Resource Group.

- Go to the "Advanced" tab, under Data Lake Storage Gen2, switch "Hierarchical namespace" to enabled. 

<kbd> ![Advanced - Data Lake](https://user-images.githubusercontent.com/61860904/107546594-c5e8ec00-6b89-11eb-87c3-a78f8dd7271f.PNG) </kbd>

- Press "Review + Create", then press "Create".

- Once the resource has been created click on it within your resource group.

<br/>
<br/>

## 3. Load data from on premises into Azure Data Lake


- To create a new container for the CSV files, search "Containers" or scroll down to "Data Lake Storage" and select "Containers".

<kbd> ![Find Containers](https://user-images.githubusercontent.com/61860904/107547156-60e1c600-6b8a-11eb-8ccc-7b598ce9b3d1.PNG) </kbd>

- Click "+ Container"

<kbd> ![Create Container](https://user-images.githubusercontent.com/61860904/107547494-bddd7c00-6b8a-11eb-9db6-f2a99b1785a7.PNG) </kbd>

- On the right hand side of the page a window will open to name your new container.

<kbd> ![Naming Container](https://user-images.githubusercontent.com/61860904/107547618-e1a0c200-6b8a-11eb-94b9-5812771c2819.PNG) </kbd>

- Give it a name, I named mine CSVFiles.

- You now have a Container within the Data Lake to upload data into. From here you can upload data or create directories within the Lake.

- Press to the upload button to start adding data to your Data Lake.

<kbd> ![Upload to DL](https://user-images.githubusercontent.com/61860904/107547938-49efa380-6b8b-11eb-9969-4379097518c0.PNG) </kbd>

- A window will open on the right side of the page 

<kbd> ![Upload Data](https://user-images.githubusercontent.com/61860904/107548197-976c1080-6b8b-11eb-8f3b-82ce38edd5a0.PNG) </kbd>

- Choose the file you wish to upload and repeat this process until you have all the data in the Data Lake.


Congrats! Your have created the Data Lake and have all your data in the cloud.

<br/>
<br/>


## 3. Create Azure SQL Database:

- Go back to the Resource Group and press "Add" as you did for the container.

- This time we want to add a SQL Database

<kbd> ![Add SQL DB](https://user-images.githubusercontent.com/61860904/107552680-1152c880-6b91-11eb-96cf-c3d7ca283b33.PNG) </kbd>

- As per the Data Lake, choose your subscription and Resource Group, name your database and choose the server. Choose the compute and storage.

- Choose "Networking" and select "Allow Azure services and resources access this server"

<kbd> ![Firewall Azure Access](https://user-images.githubusercontent.com/61860904/107553178-ad7ccf80-6b91-11eb-92f2-770a8e582078.PNG) </kbd>

- Review + Create your SQL database

- Create the tables you will need for the CSV files to import into the SQL Database, select Query Editor in the left hand menu, this can also be done automaticallly later when we create the pipline.

<kdb> ![Query Editor](https://user-images.githubusercontent.com/61860904/107558163-b2dd1880-6b97-11eb-8a56-b75df32298ff.PNG) </kbd>

- Login to your database and you can run queries to create the tables required usign the CREATE TABLE command.

- Ensure the columns have the correct data type or you will have errors moving the data to the SQL Database, remember that CSV files are all strings by default. 


<br/>
<br/>

## 4. Use Azure Data Factory to move data

- The source and sink destinations complete.

- Now we need to implement a Azure Data Factory to move the data for us.

- As before, go to "add" and search for "factory"

<kbd> ![Create Data Factory](https://user-images.githubusercontent.com/61860904/107554498-42cc9380-6b93-11eb-8926-c3931dd23b8e.PNG) </kbd> 

- Again enter your subscription and Resource Group, choose your region, give it a name and make sure you are using V2.

- You can configure your Data Factory to git in the "Git configuration" tab.

- Once the Data Factory has been created, open it and select "Author & Monitor".

<kbd> ![DF Author   Monitor](https://user-images.githubusercontent.com/61860904/107554963-d900b980-6b93-11eb-9589-86707d1e349a.PNG) </kbd> 

- First we need to make our linked services to both the Data Lake and the SQL Database.

- Go to the Toolkit with a wrench icon on the left hand menu (Manage)

<kbd> ![Pencil Icon](https://user-images.githubusercontent.com/61860904/107557587-0b5fe600-6b97-11eb-88f5-d96c5b78ead9.PNG) </kbd>

- Select "New".

<kbd> ![New Linked Service](https://user-images.githubusercontent.com/61860904/107561803-3a2c8b00-6b9c-11eb-9e58-a9258a55ecea.PNG) </kbd>

- Choose Azure Data Lake Gen2 from the list.

- Name it appropriately (e.x. Input DL).

- Choose your Azure subscription and the Data Lake where the CSV files are.

- Test Connection and then create it.

- Repeat this process selecting Azure SQL Database and inputting the login for your SQL Database.

- Now that the linked services are completed, you will need datasets to tell what the data contains.

- Select the pencil icon (Author) in the left hand side menu

<kbd> ![Pencil Icon](https://user-images.githubusercontent.com/61860904/107557587-0b5fe600-6b97-11eb-88f5-d96c5b78ead9.PNG) </kbd>

- Select the three dots beside Datasets and choose "New Dataset"

<kbd> ![New Dataset](https://user-images.githubusercontent.com/61860904/107562800-83c9a580-6b9d-11eb-822e-99e67e153dc7.PNG) </kbd>

- A window will open on the right hand side of the page, we need to tell the pipline where the data is coming from. Scroll down to "Azure Data Lake Storage Gen2".

<kbd> ![ADL Storage Dataset](https://user-images.githubusercontent.com/61860904/107653637-166e5100-6c3f-11eb-8fad-46d3fc2c07f9.PNG) </kbd>

- Now select the data type in the Date Lake, we have CSV's.

<kbd> ![CSV in ADL](https://user-images.githubusercontent.com/61860904/107653822-474e8600-6c3f-11eb-9618-24a9f13bdfb7.PNG) </kbd>

- Press continue and give the dataset a name and choose the linked service to our Data Lake we just created above.

- Choose the "First row as header" if it aplicable to your dataset.

- We need to repeat this to build the dataset for the SQL Database.

- Select "New Dataset", this time scroll down to "Azure SQL Database.

<kbd> ![SQL DB Dataset](https://user-images.githubusercontent.com/61860904/107654428-e4a9ba00-6c3f-11eb-8786-4363308fb7ba.PNG) </kbd>

- Choose a name and the linked service for the SQL Database.

- Now we can create our pipline.

- Select the three dots beside Pipelines and "New Pipeline".

- On the right hand side of the page a window will open to name your pipeline.

<kbd> ![New Pipeline](https://user-images.githubusercontent.com/61860904/107655220-9a750880-6c40-11eb-8ca9-5aa62782f905.PNG) </kbd>

- We are copying data from the CSV files to the SQL Database so open "Move & transform".

- Drag "Copy data" into the main pipeline space.

<kbd> ![Copy  Data](https://user-images.githubusercontent.com/61860904/107655958-f63f9180-6c40-11eb-9c3b-5922bc3a198d.PNG) </kbd>

- A menu will open below the pipeline, from here you can name the activity and set the source / sink datasets.

- Select Source.

<kbd> ![Source Dataset](https://user-images.githubusercontent.com/61860904/107656845-ca70db80-6c41-11eb-839b-75367aaec5e5.PNG) </kbd>

- Choose the dataset that is the source, the CSV dataset in our case.

- Select Sink

<kbd> ![Sink Dataset](https://user-images.githubusercontent.com/61860904/107656965-e96f6d80-6c41-11eb-8d94-9b7684dd0a99.PNG) </kbd>

- Choose the dataset that is the sink, the SQL Database dataset in our case.

- From here, if you did not create the table in your SQL Database, choose the option "Auto create table"

<kbd> ![Auto Create Table](https://user-images.githubusercontent.com/61860904/107657314-4e2ac800-6c42-11eb-96d5-c89b4e6997ef.PNG) </kbd>

- In the "Mapping" tab, you can import the table schema and ensure that the data types line up, if they are not compatable, your pipeline will fail.

<kbd> ![Import Schema](https://user-images.githubusercontent.com/61860904/107657616-8b8f5580-6c42-11eb-9bc0-cae22ba1393a.PNG) </kbd>

- Once the data types all match we can try and debug the pipeline to see if it will run.

<kbd> ![Debug Pipeline](https://user-images.githubusercontent.com/61860904/107657921-dd37e000-6c42-11eb-900c-82cfa3a81df9.PNG) </kbd>

- It will display successful in the bottom menu when the debugger has finished successfully.

<kbd> ![Debug Success](https://user-images.githubusercontent.com/61860904/107661017-145bc080-6c46-11eb-8397-4bf1dc94143c.PNG) </kbd>

<br/>
<br/>

You have now successfully setup your Azure Data Factory Pipeline!

<br/>
<br/>


## 5. Use Power BI to analyse data in Azure SQL Database

- Open Power BI desktop, select "Get data" from the ribbon at the top

<kbd> ![PBI Get Data](https://user-images.githubusercontent.com/61860904/107661638-b1b6f480-6c46-11eb-8781-49db991c47ae.PNG) </kbd>

- Select the More option.

- Choose Azure and select Azure SQL Database.

<kbd> ![PBI Get Data Azure SQL](https://user-images.githubusercontent.com/61860904/107663628-d14f1c80-6c48-11eb-94ee-a6a4807795c0.PNG) </kbd>

- Enter your server name, which can be found in the resource in Azure, choose the SQL Database and under the "Essentials" tab.

- You need to login to your SQL server using the same login used in teh SQL Database in Azure.

- The "Navigator" window will open up and select the tables you wish to import to Power BI

- From here you can either "Transform" the data if there is changes to be made or you can "Load" the data if it is already to be used in analysis.


<br/>
<br/>

I have included examples of visuals you can make from a climbing data set that I used.

<br/>
<br/>

<kbd> ![PBI Page 1](https://user-images.githubusercontent.com/61860904/107666579-e8dbd480-6c4b-11eb-9ace-52365805ddc7.PNG) </kbd>

<br/>
<br/>

<kbd> ![PBI Page 2](https://user-images.githubusercontent.com/61860904/107666621-f2fdd300-6c4b-11eb-986f-08f74d7b91e7.PNG) </kbd>

<br/>
<br/>

<kbd> ![PBI Page 3](https://user-images.githubusercontent.com/61860904/107666655-fb560e00-6c4b-11eb-8eca-5bb641511f7d.PNG) </kbd>






