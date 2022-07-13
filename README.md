# Utopia Backend Test


Welcome to the Utopia backend exercise! The aim is to demonstrate knowledge of the .NET Core ecosystem and integration with SQL server.

### Setup

This repo contains a (mostly) unmodified copy of the Visual Studio example project for .NET Core web api.
We have also setup a public SQL database that you can connect to for this exercise.

``
ConnectionString: "Server=tcp:backend-dev-test.database.windows.net,1433;Initial Catalog=utopia;Persist Security Info=False;User ID=candidate;Password=FairPayForEveryPlay!" ``


1) Fork and clone this repo using an IDE of you choice
2) Use the dotnet CLI to auto-scaffold the database using the connection string
* Don't worry that it skips some of the columns with user defined types

### Challenge

When you have completed the setup you should have a project that has a database context and starts with an autogenerated swagger api where you can test your controller.
We would like you to use LINQ and Async methods where appropriate.

Here are the tasks:
1) Create a new controller, use DI to make the database context available to your actions
2) Create an endpoint on your controller 
   * GET `SearchCustomers`
   * Inputs: query (string)
   * Returns: A list of rows from `SalesLT.Customer` where `query` is a partial match on `Customer.CompanyName` or `Customer.SalesPerson`. Do not include `PasswordHash` or `PasswordSalt` in results.

3) Create an endpoint on your controller
   * GET `TopSalesPeople`
   * Inputs: *None*
   * Returns: A distinct list of all sales people (found in `Customer.SalesPerson`) ranked by how much money they have earned the company in (`SalesOrderHeader.TotalDue`). Each row should also include the total number of units sold (`SalesOrderDetail.OrderQty`) and a nested list of the top products they have sold.
   * You should use at least one LINQ join, but you do not need to fetch all the data in a single query.
   * Your response should look somthing like this.
```javascript
[
   {
      "SalePerson": "adventure-works\\jae0 ",
      "TotalEarned": 22659222.5254,
      "TotalItems" : 1172,
      "TopProducts": [
        {
          "ProductID": 707,
          "Sold": 4
        },
        ...
      ]
    },
   {
      "SalePerson": "adventure-works\\linda3",
      "TotalEarned": 7495573.6309,
      "TotalItems" : 578,
      "TopProducts": [
        {
          "ProductID": 938,
          "Sold": 4
        },
        ...
      ]
    },
    ...
  ]
```

3) Create an endpoint on your controller
   * GET `RickAndMortyChars`
   * Inputs: query (string)
   * Returns: Executes a request to [this api](https://rickandmortyapi.com/documentation/#filter-characters) and returns the result. Use the `query` input string to filter the characters using the instructions in the api docs. Return the json in the same form it comes from the api.
   * https://rickandmortyapi.com/documentation/#filter-characters
   * You should use HTTPClient with DI to execute the request from your action.

### Upload your solution

Send us your solution, this can be as a Git repo or a zip - your choice.

If you have questions reach out to us at (use both emails)

* `thomas.osgood@utopiamusic.com`
* `isaac.kalil@utopiamusic.com`

Good luck!