# exercise-data-backfill
You run a SaaS business to help restaurants keep track of their sales. Everytime a purchase is made, you collect some data about the transaction.

Your client-side software had a bug last week that prevented it from collecting an important piece of information: the name of the restaurant.

You realised this a bit late and some of the incoming purchase transactions got saved with incomplete data in your database.

Luckily, you know which specific purchases have missing information and have a plan to backfill them. Since your software successfully collected the `employeeId` for all purchases, you'll use the `employeeId` to `restaurantName` relationship to infer which `restaurantName` a specific transaction belongs to.

## About your database:

Your database uses SQLite (attached `restaurants.db`) and has the following schema:

```
      +--------------------+
      | purchase_data      |
      |--------------------|
      |                    |              +--------------------+
      | id                 |              | purchases          |
      | variableName       |              |--------------------|
      | value              |              |                    |
      | purchaseId         +------------->| id                 |
      | lastModifiedDate   |              | status             |
      | createdDate        |              | lastModifiedDate   |
      |                    |              | createdDate        |
      |                    |              |                    |
      +--------------------+              |                    |
                                          |                    |
                                          +--------------------+
```

In the `purchases` table, you save all incoming purchase transactions. They get marked with a `status = "incomplete"` when one of the variable records is missing or has a value of `NULL`, and get a `status = "ok"` otherwise.

In the `purchase_data` table you collect multiple variables (`employeeId` and `restaurantName` along some others) for each purchase.

For the  `employeeId` to `restaurantName` mapping, your colleague sends you the full list of registered Employees in a CSV file (attached `employees.csv`)

## Your task

Use this information to backfill the `restaurantName` variable in the purchase_data table for the problematic purchases. Make sure to also mark
corresponding record in the purchase table by setting it's status to "ok".

To achieve your goal, you may write a script, manually run the SQL queries, use Excel or use any combination of methods you think will help you.
