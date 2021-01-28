# Workshop Mulesoft hands-on training – Use cases

Needed for the use cases:
Input:
-	Books_v1.0.0.xsd
-	Books_v1.0.0_OK.xml
-	Books_v1.0.0_NOK.xml
-	Books_v1.0.0_OK_UnkownPubl.xml
-	books-api-adri.raml
-	publishers-api-adri.raml
-	addressType.raml
-	bookType.raml
-	publisherType.raml
-	regionType.raml
-	writerType.raml
-	getBooksResponse.raml
-	getPublishersResponse.raml
-	getSingleBookResponse.raml
-	getSinglePublisherResponse.raml
-	postSingleBookRequest.raml
-	postSinglePublisherRequest.raml

On Cloudhub, environment 
Training:
•	books-ws (http://books.de-c1.cloudhub.io/console/)
•	publishers-ws (http://publishers.de-c1.cloudhub.io/console/)

Pre req:
Clone GIT repo for WorkShop

-	Create the applications in such a manner that a can be published to different environments.
-	Register the apis so that policies can be applied in the future.
-	Use encryption and secured property configuration files.
-	Use global and environment specific config files.

The applications need to be developed in a way that they can be released in production. (Naming conventions, organizing code, correct functionality).

Use case 1:

Steps:
1 – Create Anypoint MQ queues
Create two queues, one queue to store the contents of input file and one queue to store separate books. All queues must also have an error queue. Use descriptive names for the queues.
Use your companies naming convention in creating the queues.


2 – Create service
Create a service that reads the Books_v1.0.0._OK.xml file from an input directory. 
A successful processed file must be moved to an archive directory. If an error occurs, the file must be moved to an error directory. The moved file’s name  must be extended with a datetimestamp.
The directory locations are free to choose.

Each input file must be validated to the Books_v1.0.0.xsd.

Processing the file consists of these steps:
1.	Write the contents of the orderfile as is (XML format) to the content queue which stores the contents of a file.
2.	For each publisher in the input file call the webservice publishers-ws to check if the publisher exists.
3.	If the publishers does not exist, add the publisher using the same webservice.
4.	The books will need to be converted in the respected CDM datamodels of the books-ws API.
5.	For each book in the input file write the book as a JSON to the queue for separate books.

3 – Check functionality
Is the error handling correctly implemented.
Write a unit test checking a dataweave transformation or subflow.
Write a positive and a negative test.

Use case 2:

Purpose: subscribe.

Steps:
1 – Create service to read the books queue.

2 – For each books:
-	Check if the book exists using the books-ws service. 
-	If not, add the book using the books-ws service.
-	If any error occurs, use the error queue.

Note: 
-	Decide how to check the existence of the book and why.
-	Use circuit breaker to stop the processing in case of a transient Error

3 – Check functionality
Is the error handling correctly implemented.
Write a unit test checking the dataweave transformation.
Write a positive and a negative test.


Use case: 3: Advanced functionality

2 – Add complex error handling.
-	For instance, should you scope the error handling to a flow or not
-	Or do you think you need error handling on several level? Why?

3- Add in track and trace of messages. How will you approach this?


Use case 4: Releasing APIs

Before API’s are released the 4-eye principle is being used.
-	In order for the API’s to be released check each others solution?
-	What could be improved and what is written in a positive manner?

Demonstrate your API’s and explain the design decisions you made.


