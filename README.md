# ClimbingProject

## Process Outline:
1. Create Resource Group 
2. Load data from static CSV files into Azure Data Lake Gen2
3. Create Azure SQL Database
4. Use Azure Data Factory to move CSV data into a Azure SQL Database
5. Use Power BI to analyse data in Azure SQL Database


<br/>
<br/>
Lets start at the Azure portal home page:  https://portal.azure.com/
<br/>
<br/>

## 1. Create Resource Group

- We need to create a resource group to have all the Azure products in one place.

- Select the Resource Groups icon: 

<kbd> ![Resource Groups](https://user-images.githubusercontent.com/61860904/107544144-262a5e80-6b87-11eb-9eed-ad42ff619ae8.PNG) </kbd>

- Then create one.

<kbd> ![Create Resource Group](https://user-images.githubusercontent.com/61860904/107544611-a5b82d80-6b87-11eb-8c03-6333e8a7c414.PNG) </kbd>

- Select your subscripton and give the Resource Group a name, then choose the region closest to you.

- Review+Create your Resource Group

<br/>
<br/>

## 2. Load Data into Azure Data Lake Gen2 

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

- Go to the "Advanced" tab and select Data Lake Storage Gen2. 

<kbd> ![Advanced - Data Lake](https://user-images.githubusercontent.com/61860904/107546594-c5e8ec00-6b89-11eb-87c3-a78f8dd7271f.PNG) </kbd>

- To create a new container for the CSV files, search "Containers" or scroll down to "Data LakeStorage"

<kbd> ![Find Containers](https://user-images.githubusercontent.com/61860904/107547156-60e1c600-6b8a-11eb-8ccc-7b598ce9b3d1.PNG) </kbd>

- Click "+ Container"

<kbd> ![Create Container](https://user-images.githubusercontent.com/61860904/107547494-bddd7c00-6b8a-11eb-9db6-f2a99b1785a7.PNG) </kbd>

- On the right hand side of the page a window will open to name your new container.

<kbd> ![Naming Container](https://user-images.githubusercontent.com/61860904/107547618-e1a0c200-6b8a-11eb-94b9-5812771c2819.PNG) </kbd>

- Give it a name, I named mine CSVFiles.

- You now have a Data Lake to upload data into. From here you can upload data or create directories within the Lake.

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

