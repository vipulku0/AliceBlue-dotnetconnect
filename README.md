<h1>Alice Blue .Net library</h1>

The official .Net client for communicating with Alice Blue API.

Alice Blue is a set of REST-like APIs that expose many capabilities required to build a complete investment and trading platform. Execute orders in real time, manage user portfolio, and more, with the simple HTTP API collection.

© 2022 Alice Blue. All rights reserved.

<hr>

<h1>Requirments</h1>

AliceBlue targets netstandard2.0. Minimum project target is .NET Core 3.1.

<hr>

<h1>Documentation</h1>

.Net Library

<h1>Getting started</h1>

// Import library
using KiteConnect;

// Initialize Kiteconnect using apiKey. Enabling Debug will give logs of requests and responses
Kite kite = new Kite(MyAPIKey, Debug: true);

// Collect login url to authenticate user. Load this URL in browser or WebView. 
// After successful authentication this will redirect to your redirect url with request token.
kite.GetLoginURL();

// Collect tokens and user details using the request token
User user = kite.GenerateSession(RequestToken, MySecret);

// Persist these tokens in database or settings
string MyAccessToken = user.AccessToken;
string MyPublicToken = user.PublicToken;

// Initialize Kite APIs with access token
kite.SetAccessToken(MyAccessToken);

// Set session expiry callback. Method can be separate function also.
kite.SetSessionExpiryHook(() => Console.WriteLine("Need to login again"));

// Example call for functions like "PlaceOrder" that returns Dictionary
Dictionary<string, dynamic> response = kite.PlaceOrder(
    Exchange: Constants.EXCHANGE_CDS,
    TradingSymbol: "USDINR17AUGFUT",
    TransactionType: Constants.TRANSACTION_TYPE_SELL,
    Quantity: 1,
    Price: 64.0000m,
    OrderType: Constants.ORDER_TYPE_MARKET,
    Product: Constants.PRODUCT_MIS
);
Console.WriteLine("Order Id: " + response["data"]["order_id"]);

// Example call for functions like "GetHoldings" that returns a data structure
List<Holding> holdings = kite.GetHoldings();
Console.WriteLine(holdings[0].AveragePrice);





