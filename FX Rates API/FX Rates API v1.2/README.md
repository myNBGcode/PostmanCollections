# **Introduction**
#### Welcome to the Fx Rates Sandbox API.

------------------------------------------------------------------------------------------
### A few words about rates
In finance, an exchange rate is the rate at which one currency will be exchanged for another. It is also regarded as the value of one country’s currency in relation to another currency. For example, an interbank exchange rate of 114 Japanese yen to the United States dollar means that ¥114 will be exchanged for each US$1 or that US$1 will be exchanged for each ¥114. In this case it is said that the price of a dollar in relation to yen is ¥114, or equivalently that the price of a yen in relation to dollars is $1/114.

> Read more at https://en.wikipedia.org/wiki/Exchange_rate

### The API
This API provides a standard RESTful interface that enables a user to
* Get the value of one country’s currency in relation to another currency
* View supported rates
* View supported currencies

> Visit https://developer.nbg.gr/documentation/FX-Rates-API-v1.2
> for the full API documentation

### Real life Use Case Scenario
In this scenario we will be using the API to provide data to the *Travel Abroad Advisor* application.

The main functionality of the application is to convert an amount in the currency of the country the user is living in - we will refer to this currency as **home currency** - to the amount in the currency of the country they will be visiting, the **foreign currency**.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/fxrates/headers/v1.2/sandbox

With a request body:
```json
 {
   "sandbox_id": "113E4C18-FA0D-49B7-992E-F90E7CC3922B"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

The available currencies can be fetched from the API by making an **HTTP GET** request to the following URL:

> https://apis.nbg.gr/sandbox/fxrates/headers/v1.2/currencies/all

The response is a JSON object containing a list of **Currency** JSON objects, as shown below.
```json
[
  {
    "currencySymbol": "USD",
    "currencyCode": "002"
  }
]
```
When user selects the *home currency* and the *foreign currency*, the application will make an **HTTP GET** request to the following URL to fetch the related rates information.
> https://apis.nbg.gr/sandbox/fxrates/headers/v1.2/fx/{fromCurrency}/{toCurrency}

The response contains a JSON **FxRates** object as shown below.
```json
{
  "currencySymbol": "USD",
  "exchangeBuy": "1.17695000",
  "exchangeSell": "1.10859000",
  "currencyCode": "002",
  "banknotesBuy": "1.17695000",
  "banknotesSell": "1.10859000"
}
```
The application will store the result and use it to calculate the amount conversion by multiplying the user input with the value of **exchangeBuy** field.

Created by **NBG**. 
See more at https://developer.nbg.gr/
