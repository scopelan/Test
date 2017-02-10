 ```java
 // Make the API Request
    CreateTransactionRequest apiRequest = new CreateTransactionRequest();
    apiRequest.setTransactionRequest(txnRequest);
    CreateTransactionController controller = new CreateTransactionController(apiRequest);
    controller.execute();

    CreateTransactionResponse apiResponse = controller.getApiResponse();

    if (apiResponse != null) {
        // If API response code is ok (transaction is successful), 
        // go ahead and check the transaction response
        if (apiResponse.getMessages().getResultCode() == MessageTypeEnum.OK) {

            TransactionResponse txnResponse = apiResponse.getTransactionResponse();
            if (txnResponse.getResponseCode().equals("1")) {
                 out.println(txnResponse.getResponseCode());
                 out.println("Successful Credit Card Transaction");
                 out.println("Auth Code: " + txnResponse.getAuthCode());
                 out.println("Transaction ID: " + txnResponse.getTransId());
            }
            else {
                 out.println("Failed Transaction. Response Code: " + 
                                            txnResponse.getResponseCode());
            }
        }
        else {
             out.println("Failed Transaction. Result Code:  " + 
                  apiResponse.getTransactionResponse().getErrors().getError().get(0).getErrorCode() +
                  apiResponse.getTransactionResponse().getErrors().getError().get(0).getErrorText());
        }
    }
  %>
  ```
