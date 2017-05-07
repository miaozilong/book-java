The`SimpleJdbcInsert`and`SimpleJdbcCall`classes provide a simplified configuration by taking advantage of database metadata that can be retrieved through the JDBC driver. This means there is less to configure up front, although you can override or turn off the metadata processing if you prefer to provide all the details in your code.

Let’s start by looking at the`SimpleJdbcInsert`class with the minimal amount of configuration options. You should instantiate the`SimpleJdbcInsert`in the data access layer’s initialization method. For this example, the initializing method is the`setDataSource`method. You do not need to subclass the`SimpleJdbcInsert`class; simply create a new instance and set the table name using the`withTableName`method. Configuration methods for this class follow the "fluid" style that returns the instance of the`SimpleJdbcInsert`, which allows you to chain all configuration methods. This example uses only one configuration method; you will see examples of multiple ones later.



