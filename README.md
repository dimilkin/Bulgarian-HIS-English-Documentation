# Bulgarian HIS (Healthcare Information System) API Documentation

## API Addresses
- **Home website of the NHIS System:** `https://his.bg/bg/dev/specifications`
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
  
### Detailed description of the API endpoints and the corresponding rules and business logic can be found in the XLSX files provided in this repo.
- Every call should be digitally signed by the same entity that obtained the authorization token - with the same certificate
- An example of a call X001 request headers and body looks like this:
```xml
  <nhis:message xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:nhis="https://www.his.bg" xsi:schemaLocation="https://www.his.bg https://www.his.bg/api/v1/NHIS-X001.xsd">
    <nhis:header>
        <nhis:sender value="[code]"/> <!--CL018-->
        <nhis:senderId value="[string]"/>
        <nhis:senderISName value="[string]"/>
        <nhis:recipient value="[code]"/> <!--CL018 - it is 4 in all cases-->
        <nhis:recipientId value="[string]"/>
        <nhis:messageId value="[string]"/>
        <nhis:messageType value="[string]"/>
        <nhis:createdOn value="[dateTime]"/>
    </nhis:header>
    <nhis:contents>
        <nhis:examination>
            <nhis:lrn value="[string]"/>
            <nhis:openDate value="[dateTime]"/>
            <nhis:class value="[code]"/>
            <nhis:financingSource value="[code]"/>
            <nhis:rhifAreaNumber value="[code]"/>
        </nhis:examination>
        <nhis:subject>
            <nhis:identifierType value="[code]"/>
            <nhis:identifier value="[string]"/>
            <nhis:birthDate value="[date]"/>
            <nhis:gender value="[code]"/>
            <nhis:name>
                <nhis:given value="[string]"/>
                <!-- Optional: -->
                <nhis:middle value="[string]"/>
                <nhis:family value="[string]"/>
            </nhis:name>
            <nhis:address>
                <nhis:country value="[code]"/>
                <!-- Optional: -->
                <nhis:county value="[code]"/>
                <nhis:city value="[string]"/>
                <!-- Optional: -->
                <nhis:line value="[string]"/>
                <!-- Optional: -->
                <nhis:postalCode value="[string]"/>
            </nhis:address>
            <!-- Optional: -->
            <nhis:nationality value="[code]"/>
            <!-- Optional: -->
            <nhis:phone value="[string]"/>
            <!-- Optional: -->
            <nhis:email value="[string]"/>
        </nhis:subject>
        <nhis:performer>
            <nhis:pmi value="[string]"/>
            <!-- Optional: -->
            <nhis:pmiDeputy value="[string]"/>
            <nhis:qualification value="[code]" nhifCode="[code]"/>
            <nhis:practiceNumber value="[string]"/>
            <nhis:role value="[code]"/>
            <!-- Zero or more repetitions: -->
            <nhis:accompanying>
                <nhis:pmi value="[string]]"/>
                <nhis:qualification value="[code]" nhifCode="[code]"/>
            </nhis:accompanying>
            <!-- Optional: -->
            <nhis:phone value="[string]"/>
            <!-- Optional: -->
            <nhis:email value="[string]"/>
            <!-- Optional: -->
            <nhis:rhifAreaNumber value="[code]"/>
            <!-- Optional: -->
            <nhis:nhifNumber value="[string]"/>
        </nhis:performer>
    </nhis:contents>
    <Signature/>
</nhis:message>
```
This documentation will be updated over time.

