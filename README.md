# LT_Upload_Chrome_Profile_Remote_driver
This repo includes the steps to upload a custom profile in LambdaTest remote driver on Chrome browser.

**Chrome profile can be passed with local Chrome driver using chromeOptions like below; however, the same was not supported with the remote driver.

chromeOptions option = new ChromeOptions();

 option.addArguments("user-data-dri=C:\\Users\\Your path to user\\Roaming\\Google\\Chrome\\User Data"); 

WebDriver driver = new ChromeDriver(option);**

 

We have developed a capability called browserProfile through which users can upload a custom profile for their LambdaTest automation tests. 

Steps:

Compress the custom Chrome profile folder and then use the below API to upload it to the LambdaTest cloud storage:

curl --location --request POST 'https://api.lambdatest.com/automation/api/v1/files/profile/chrome' \

--header 'Authorization: Basic xxxxxx' \

--form 'profile=@"/Users/abc/Desktop/zip.zip"'

Note: Chrome profile path C:\Users\abidk\AppData\Local\Google\Chrome\User Data. 


After uploading the compressed file, a URL like https://automation-prod-user-files.s3.amazonaws.com/profile/chrome/orgId-2939/zip.zip will be generated.

You can pass this URL with the below capability in your script and you are good to go.

"browserProfile":"https://automation-prod-user-files.s3.amazonaws.com/profile/chrome/orgId-242939/zip.zip"




We also have 2 other APIs to see the list of uploaded profiles and to delete them.
 
1. Curl request to get the list of profiles:

curl --location --request GET 'https://api.lambdatest.com/automation/api/v1/files/profile/chrome' \

--header 'Authorization: Basic xxxxx' \

--form 'profile=@"/Users/abc/Desktop/zip.zip"'

 

 

2. Curl request to delete profiles:

curl --location --request DELETE 'https://api.lambdatest.com/automation/api/v1/files/profile/chrome' \

--header 'Authorization: Basic xxxx' \

--header 'Content-Type: application/json' \

--data-raw '{"key": "zip.zip"}'

 

NOTE
*The compressed zip file can be a max of 100 MB now(updated).

*Make sure the exact profile folder is zipped. If you zip the parent folder or subfolder, the functionality won’t work.
