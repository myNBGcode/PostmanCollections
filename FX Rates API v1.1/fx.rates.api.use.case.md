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

> Visit https://microsites.nbg.gr/developer/documentation/87b7b6df-1290-4070-bb01-99011758f6d2 
> for the full API documentation

### Real life Use Case Scenario
In this scenario we will be using the API to provide data to the *Travel Abroad Advisor* application.

The main functionality of the application is to convert an amount in the currency of the country the user is living in - we will refer to this currency as **home currency** - to the amount in the currency of the country they will be visiting, the **foreign currency**.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://microsites.nbg.gr/api.gateway/sandbox/fxrates/headers/v1.1/sandbox

With a request body:
```
 {
   "sandbox_id": "113E4C18-FA0D-49B7-992E-F90E7CC3922B"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

The available currencies can be fetched from the API by making an **HTTP GET** request to the following URL:

> https://microsites.nbg.gr/api.gateway/sandbox/fxrates/headers/v1.1/currencies/all

The response is a JSON object containing a list of **Currency** JSON objects, as shown below.
```
[
  {
    "DELT_LEKT": "USD",
    "DELT_NOM": "002"
  }
]
```
When user selects the *home currency* and the *foreign currency*, the application will make an **HTTP GET** request to the following URL to fetch the related rates information.
> https://microsites.nbg.gr/api.gateway/sandbox/fxrates/headers/v1.1/fx/{fromCCY}/{toCCY}

The response contains a JSON **FxRates** object as shown below.
```
{
  "DELT_LEKT": "USD",
  "DELT_ECBREF": "1.12810000",
  "DELT_TAS": "1.16729000",
  "DELT_TPS": "1.09949000",
  "DELT_NOM": "002",
  "DELT_TAXT": "1.16729000",
  "DELT_ETEREF": "1.13000000",
  "DELT_TPXT": "1.09949000"
}
```
The application will store the result and use it to calculate the amount conversion by multiplying the user input with the value of **DELT_TAS** field.

Created by **NBG**. 
See more at https://www.nbg.gr/