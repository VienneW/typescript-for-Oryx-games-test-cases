# typescript-for-Oryx-games-test-cases
Testing oryx games is a bit different from testing tgg games, Oryx games use POST every time with a xml body.

Call API like this:

authenticate_token_async = (json) => {
        let xml_body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:agg="API_link"><soapenv:Header/><soapenv:Body><agg:TransactionChange><agg:transactionChangeData><agg:apiAuthentication><agg:username>'+json.username+'</agg:username><agg:password>'+json.password+'</agg:password></agg:apiAuthentication><agg:token>'+json.token+'</agg:token><agg:transactionChange>'+json.transactionChange+'</agg:transactionChange><agg:transactionId>'+json.transactionId+'</agg:transactionId></agg:transactionChangeData></agg:TransactionChange></soapenv:Body></soapenv:Envelope>';
        let option = {
            method: "POST",
            url: this.url,
            body: xml_body,
            headers:{
                "Content-Type":"application/xml"
            }   
        }
        // console.log("************* authenticate_token_async INPUT ************* \n", option)
        // console.log(" ")
        return rp(option);
    }


Get response like this:

let auth_xml = await api.authenticate_token_async(authenticate_token_object);
let auth_json = parser.toJson(auth_xml);
auth_json = JSON.parse(auth_json);
let auth_res_data = auth_json["soap:Envelope"]["soap:Body"]["AuthenticateTokenResponse"]["authenticateTokenResponseData"];
