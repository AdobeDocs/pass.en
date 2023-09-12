---
title: Report API
description: Auditude report API
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
---
# Report API {#report-api}

User Interface has managed roles for customers and for the enablement (Adobe) team. Customers can access the portal, and can then create and edit their configurations. They can also see the reports for their ads impressions on the user interface.

APIs work behind the scenes to facilitate customers and administrators in communicating with the backend infrastructure.

To explore the [!DNL Primetime Ad Insertion] APIs see [Ad Insertion API endpoints in swaggered user interface](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## API endpoint {#report-api-endpoint}

### Production {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Query Parameters


|     Name |     Significance                                                                              |     Value Type |     Mandatory? |     Default   Value |     Constraints                                                                    |     Example/   Valid Sample values                                      |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate  | Ending date for the report data                                                               | date           | Y              | NONE                | not newer than yesterday in UTC-8                                                  | ########                                                                |
| filters  | filter on one or more columns                                                                 | string         | N              | NONE                | ad_config_id , zone_id                                                             | ad_config_id=990,900;state=active                                       |
|          |                                                                                               |                |                |                     | When metaData is set to 'true' in the request, then you can also   filter by name. |                                                                         |
|          |                                                                                               |                |                |                     |                                                                                    | Multiple filter   keys are semi-colon separated.                        |
|          |                                                                                               |                |                |                     |                                                                                    | Use   comma-separated values to provide a list of values for filter key |
| groupBy  | Group by on time ( year \| month \|   day) or ad_config_id. Adconfig is synonymous of AdRule. | string         | N              | NONE                |  y \| m \| d  ,   ad_config_id                                                     | m , ad_config_id                                                        |
|          |                                                                                               |                |                |                     |                                                                                    |                                                                         |
|          |                                                                                               |                |                |                     |                                                                                    | For groupBy on time provide either one of  y or m or d                  |
|          |                                                                                               |                |                |                     |                                                                                    |                                                                         |



## Headers {#headers}

|         Name          |     Value type |     Mandatory |     Sample value                    |     Significance                   |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Accept                | string         | Y             | text/csv  for CSV                   | Type of response expected from API |
|                       |                |               | application/json or '*/*'  for JSON |                                    |
| Authorization   token | string         | Y             | xyz                                 | authorization token                |
| x-api-key             | string         | Y             | xyz                                 | API key                            |
| x-gw-ims-org-id       | string         | Y             | xyz12345                            | IMS org Id of your account         |

* You can generate the Authorization token (also known as access token) by following the steps detailed out in Adobe.io's JWT authentication help-page.
  >
  >[!NOTE]
  >Authorisation token has an expiry of 24 hours, so if you are using Report API using a recurring script, then make sure you generate auth token before its expiry or when you get an Oauth error about token not being valid.

* To set the correct values in the request header and to generate Authorization token (using JWT authentication) you will need to know the below configurations for your account. Please get in touch with Primetime Support team to get these values.
Technical account id

  * Org id
  * Api_key
  * Client_secret

## Output {#output}

The result of Report API query by default is in JSON format which specifies impressions against the different values of the dimensions (groupby param) requested. Sample output is given below:

```JSON

[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Error Codes and Strings {#error-codes-strings}

### Error Response Format {#error-response-format}

Error rendering macro 'code': Invalid value specified for parameter `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

The table below lists down the Error codes and messages that Report API can return. For errors related to authorization layer, refer the [error code documentation](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) of Adobe.io.

|         Error Code    |     Error   Message                      |
|-----------------------|------------------------------------------|
| 4001007               | User   detail is invalid.                |
| 4001008               | All   zones are not from same account.   |
| 5001010               | An   internal error occurred.            |
| 4001011               | Dates   are not sent in required format. |
| 4001012               | Dates   are out of range.                |
| 4001013               | Mandatory   Parameter is missing.        |
| 4001014               | Zone   list is empty for the account.    |
| 4001015               | Invalid   Filter keys in request.        |
| 4001016               | Invalid   GroupBy option in request.     |
| 4001017               | Invalid   ID is provided in request      |

## Sample Calls and expected results {#sample-calls-expected-results}

Following is the curl command to get monthly impression counts between 2020-07-01 and 2021-06-30 using access token:

**Reporting API call example**

```shell

curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'

```

| Sample Call/ Use case | Expected Result |
|---|---|
| Fetch Report with start and end dates  GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2021-01-01 header : Accept = application/json. or */*                                                                |  Json with following parameters with all the ads belonging to this account total_impressions                                                                |
| Fetch Report with GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&endDate=2020-05-01&groupBy=d \| m \| y header : Accept = application/json. or */*                                          |  Json with following parameters with all the ads belonging to this account  dates (mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions                  |
| Fetch Report with GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-05-01&groupBy=ad_config_id header : Accept = application/json. or */*                                         |  Json with following parameters with all the ads belonging to this account  ad_config_id total_impressions                                                  |
| Fetch Report with GroupBy =  d \| m \| y and  ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-05-01&groupBy=d,ad_config_id header : Accept = application/json. or */*                     |  Json with following parameters with all the ads belonging to this account  ad_config_id dates (mm-dd-yyyy \| mm-yyyy \| yyyy format) total_impressions     |
| Fetch Report with metaData=true and groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-05-01&metaData=true&groupBy=ad_config_id header : Accept = application/json. or */*            |  Json with following parameters with all the ads belonging to this account ad_config_id name total_impressions                                              |
| Fetch Report with groupBy=d \| m \| y and ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-05-01&metaData=true&groupBy=d \| m \| y,ad_config_id header : Accept = application/json. or */* |  Json with following parameters with all the ads belonging to this account ad_config_id name total_impressions dates (mm-dd-yyyy \| mm-yyyy \| yyyy format) |
| Fetch Report to get all the rows for a given date range (with unpaged = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-31&groupBy=d&unpaged=true                                             |  31 entries in the returned Json array                                                                                                                      |
| Fetch Report with valid page query parameters GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-31&page=0&size=5&groupBy=d                                                                            |  5 entries in the returned array                                                                                                                            |
| Fetch Report, with csv format GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-10 header : Accept = text/csv                                                                                         |  CSV string is returned, with header: total_impressions                                                                                                     |
| Fetch Report, with csv format , and groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-10&groupBy=d\|m\|y header : Accept = text/csv                                             |  CSV string is returned, with header: total_impressions dates (mm-dd-yyyy \| mm-yyyy \| yyyy format)                                                        |
| Fetch Report, with csv format , and metadata = true GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-10&metaData=true header : Accept = text/csv                                                     |  CSV string is returned, with header: total_impressions                                                                                                     |
| Fetch Report, with csv format , metadata = true, and groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&endDate=2020-01-10&metaData=true&groupBy=d\|m\|y header : Accept = text/csv              |  CSV string is returned, with header: total_impressions dates (mm-dd-yyyy \| mm-yyyy \| yyyy format)                                                        |


## Report API Throttling Policy {#report-api-throttling-policy}

* 5 API requests are allowed during a 5 second window for each user.
* If a user crosses above limit, response is delayed by 5 seconds.
* If a user makes more than 10 calls within 5 second window, they will start getting rejected with response "429 Too many requests".
