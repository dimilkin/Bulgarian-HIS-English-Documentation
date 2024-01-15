# Bulgarian HIS (Healthcare Information System) API Documentation

## API Addresses
- **Main Production API address:** `https://api.his.bg`
- **Test Environment API address:** `https://ptestapi.his.bg`

## Authorization
  To interact with the endpoints, a Bearer token is required for authorization.

### Obtaining the Token
- Make a GET request to the auth endpoints:
    - **Production:** `https://auth.his.bg`
    - **Test:** `https://ptest-auth.his.bg`
- The request must be signed with a valid electronic signature.
- Valid XSD schema information: [W3C XML Signature Syntax and Processing](https://www.w3.org/TR/xmldsig-core/)
- Schema location: [XML Signature Schema](http://www.w3.org/2000/09/xmldsig#)

### Successful Authentication Response
```xml
<?xml version="1.1" encoding="UTF-8"?>
<nhis:message xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:nhis="https://www.his.bg" xsi:schemaLocation="https://www.his.bg
https://www.his.bg/api/v1/NHIS-S001.xsd">
 <nhis:contents>
  <nhis:accessToken value="imSXTs2OqSrGWzsF3rF..." dataType="[string]"/>
  <nhis:tokenType value="bearer" dataType="[string]"/>
  <nhis:expiresIn value="7200" dataType="[positiveInt]"/>
  <nhis:issuedOn value="2020-10-21T18:11:23" dataType="[dateTime]"/>
  <nhis:expiresOn value="2020-10-21T18:13:23" dataType="[dateTime]"/>
 </nhis:contents>
</nhis:message>
```

- Use the received token in the headers of subsequent requests:
- `Authorization: Bearer imSXTs2OqSrGWzsF3rF...`

### Alternative Authorization Method
- If a client certificate is not included, a 401 (Unauthorized) response is received.
- The challenge message received must be signed with a valid electronic signature and sent in a POST request to the auth endpoints.
  ```xml
  <?xml version="1.1" encoding="UTF-8"?>
  <nhis:message xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:nhis="https://www.his.bg" xsi:schemaLocation="https://www.his.bg
  https://www.his.bg/api/v1/NHIS-S001.xsd">
   <nhis:contents>
    <nhis:challenge value="imSXTs2OqSrGWzsF3rF..." dataType="[string]"/>
   </nhis:contents>
  </nhis:message>

## Endpoints of the HIS
### Swagger Documentation
Access the Swagger documentation for a detailed list of functionalities: [HIS API Documentation](https://ptest-api.his.bg/index.html)
  
  ### Functionalities listed under the `EExamination` section.
1. Opening EExamination - request made with the start of the medical examination.
2. 
- 
