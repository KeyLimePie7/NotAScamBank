# Hello

This is a simple, full stack mock banking web application.
It uses DerbyDB as a database, and JDBC to connect to the DB.
It uses Spring MVC as a framework, and the application is properly split into the "Models" component, "Views" component (I used JSP templates with the JSP Standard Tag Library), and the main "Controller" component.
The entire web application can then be hosted on any web server. I used tomcat to host the web application on localhost.

It even has the feature to generate CSV and PDF files for the bank statements of our "customers"!

### Stakeholders

Let's imagine there are 2 users:

1. A new account/new customer executive
2. A cashier/teller

And we must create separate accounts with different access permissions for them.

### Scope

1. For the employee that needs to create new customer accounts

   They must be able to:

   1. Create, Update, and Delete Customers
   2. Create and Delete Cash Accounts (Each customer can have multiple cash accounts)
   3. View Customer and Account Status

2. For the cashier/teller

   They must be able to:

   1. Manage deposits, withdrawals and transfers between cash accounts
   2. Get Customer and Account details
   3. Get Customer-Account Transactions (Generate a Bank Statement)

### The Application

1. For the new-customer executive

   1. The login screen

      To allow the employee to login.
      The username can be alphanumeric with maximum n characters.
      The password can also be alphanumeric with maximum n characters.

      The input validation was done using javascript on the JSP frontend to improve user experience since feedback is instant.

      ![LoginPage](./Images/LoginPage.jpg)

   2. The "Create Customer" screen

      To allow the new-customer-account executive to create a new customer

      ![CreateCustomer](./Images/CreateCustomer.jpg)

      There is also input validation done here

   3. The "Update Customer" screen

      To allow account executive to update existing customer information

      ![UpdateCustomer](./Images/UpdateCustomer.jpg)

   4. The "Search Customer" screen

      Before the account executive can update anything, they should be able to query for existing customers

      ![SearchCustomer](./Images/CustomerSearch.jpg)

      There is also input validation done here.

   5. The "Delete Customer" screen

      To allow the account executive to delete any existing customer

      ![DeleteCustomer](./Images/DeleteCustomer.jpg)

   6. The "Delete Account" screen

      To allow the account executive to delete existing accounts.

      ![DeleteAccount](./Images/DeleteAccount.jpg)

   7. The "View Customer Status" screen

      ![CustomerStatus](./Images/CustomerStatus.jpg)

   8. The "View Account Status" screen

      ![AccountStatus](./Images/AccountStatus.jpg)

2. For the cashier/teller

   1. The "Deposit" screen

      ![DepositMoney](./Images/DepositMoney.jpg)

   2. The "Withdraw" screen

      ![WithdrawMoney](./Images/WithdrawMoney.jpg)

   3. The "Transfer" screen

      ![TransferMoney](./Images/TransferMoney.jpg)

   4. The "Get Statement" screen

      ![ViewStatement](./Images/ViewStatement.jpg)

      ![ViewStatement2](./Images/ViewStatement2.jpg)

### About the DB

DerbyDB is a full-featured relational database management system (RDBMS).
This webapp is pretty much your standard CRUD application.
We have 4 tables: loginTable, customer, account and transactions tables.

loginTable:

```java
sta.execute("CREATE TABLE loginTable (uid varchar(255), pw varchar(255))");
```

customer:

```java
String sql = "CREATE TABLE customer ("
   + " ws_cust_id int primary key NOT NULL GENERATED ALWAYS AS IDENTITY (START WITH 100000000, INCREMENT BY 1),"
   + " ws_ssn int,"
   + " name varchar(255),"
   + " ws_adrs varchar(255),"
   + " age int"
   + ")";
statement.execute(sql);
```

account:

```java
String sql = "CREATE TABLE account ("
   + " ws_acct_id int primary key GENERATED ALWAYS AS IDENTITY (START WITH 200000000, INCREMENT BY 1),"
   + " ws_cust_id int,"
   + " ws_acct_type varchar(255),"
   + " ws_acct_balance int,"
   + " ws_acct_crdate date,"
   + " ws_acct_lasttrdate date"
   + ")";
statement.execute(sql);
```

transactions:

```java
String sql = "CREATE TABLE transactions ("
   + " ws_trxn_id int primary key GENERATED ALWAYS AS IDENTITY (START WITH 300000000, INCREMENT BY 1),"
   + " ws_acct_id int,"
   + " ws_trxn_amount int,"
   + " ws_trxn_type varchar(255),"
   + " ws_trxn_date DATE"
   + ")";
statement.execute(sql);
```
