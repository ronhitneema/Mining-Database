## Mining the Database 
### Author: Ronhit Neema

#### For source code access, reach out to: neema.r@northeastern.edu, ronhitn@gmail.com

## About Loading XML to Database:
The code is written in R and is part of a database management system course project. It focuses on loading XML data into a database. Heres a breakdown of the code:

1. The code starts by loading the required libraries, including XML, RSQLite, DBI, knitr, stringr, and doParallel.

2. It defines an AWS S3 URL for the XML file to be read and stores it in the xml_url variable.

3. The XML content is read from the specified URL using the readLines() function and stored in the xml_content variable.

4. The XML content is parsed using the xmlTreeParse() function, which creates an XML document object model (DOM) stored in the xmlDOM variable. The useInternalNodes = TRUE parameter allows the parser to create new nodes for XML elements while parsing, and validate = T enables XML validation.

5. The root node of the XML document is obtained using the xmlRoot() function and stored in the r variable.

6. The code drops the existing tables (Journals, Articles, Authors, and ArticleAuthor) from the SQLite database, if they exist, using the dbSendQuery() function.

7. The code creates the necessary tables (Journals, Articles, Authors, and ArticleAuthor) in the SQLite database using the dbSendQuery() function and SQL CREATE TABLE statements.

8. Empty data frames are created for journals, articles, authors, and article-author relationships using the data.frame() function.

9. Several functions are defined, including keyExists() to check if a key exists in a data frame, rowExists() to check if a row exists in a data frame, and p() to concatenate input arguments using a specified separator.

10. The code then iterates through each publication in the XML document, extracts the required data using XPath expressions, and stores it in the respective data frames.

11. For each publication, the code checks if the journal already exists in the journal data frame. If not, a new row with journal information is added to the data frame.

12. Finally, the extracted data is saved into the appropriate tables in the SQLite database using the dbWriteTable() function.

Overall, the code loads XML data from a specified URL, parses it, extracts the required information, and stores it in a relational database using SQLite.


## Datawarehouse Loading:
The R script connects to a MySQL database and performs operations to create and populate a snowflake schema for journal facts. 
It queries a SQLite database to retrieve article author and journal information. 
It creates a new schema and tables in the MySQL database to store the data. 
The script calculates quarter, month, and year identifiers for each journal entry and updates the data accordingly. 
It retrieves article counts per month, quarter, and year and merges them with the journal facts data. 
The script replaces missing values with 0 and writes the resulting data frame to a table in the MySQL database. 
Finally, it disconnects from the database.


## Running Analytical Queries

This code in R Markdown document focuses on analyzing journal articles in a MySQL data warehouse. The document connects to the MySQL data warehouse, executes two analytical queries, visualizes the results, and provides analysis and explanations.

The first analytical query aims to find the top five journals with the most articles published. It retrieves data from the 'JournalFact' table and presents the top five journals based on the number of articles published. The resulting data frame is displayed, and bar charts are generated to visualize the total articles per quarter by journal and the articles per journal per quarter.

The second analytical query focuses on the number of articles per journal per year broken down by quarter. It retrieves data for the year 1978 and filters the results based on the articles published. The resulting data frame is displayed, and a stacked bar chart is generated to visualize the articles per journal per quarter.

For each query, analysis and interpretations are provided to highlight key findings such as the journal with the most articles, the quarter with the fewest articles, and the year with the highest number of articles. The document also discusses the choice between table and visual representation based on the dataset size and analysis goals.

Finally, the document disconnects from the MySQL data warehouse.

Please note that the code provided here assumes the availability of the necessary packages and a functional connection to the specified MySQL data warehouse.