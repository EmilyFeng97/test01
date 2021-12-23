
## Walkthrough Steps

1. File > New Project > Blazor WebAssembly App > Give a project name > select ".NET 7.0" > Checking "ASP.NET Core hosted" and change Authentication to "Individual User Accounts" > Create

    ![Project template](_images/ClientBlazorWithIndAuth/Create.png)

1. Verify there are no errors or warnings in Error List after project creation.

### Build and run

1. Build the project, verify there are no errors or warnings in Error List.

1. Run the project (F5), validate the application loads and that Register and Log in are shown in the top right corner of the screen.

    ![Verify every links](_images/ClientBlazorWithIndAuth/F5.png)

1. Press the fetch data option on the left side of the page, it will be redirected to login page if you don't log in.

    ![Verify every links](_images/ClientBlazorWithIndAuth/Login_page_F5.png)

1. On the login page, click the register as a new user link. Then register a new account and log in.

    - Note: You will initially get this screen below. This is expected. If you hit "Apply Migrations" button, then refreshing the page. Then you should confirm your email and you will get a new account. Log in using the same account.

    ![Verify every links](_images/ClientBlazorWithIndAuth/Apply_Migration.png)

    - Validate the application is redirected back to the `/fetchdata` page.

    ![Verify every links](_images/ClientBlazorWithIndAuth/Login_F5.png)

1. Click on the user name and you will be sent to the profile page.

    ![Verify every links](_images/ClientBlazorWithIndAuth/profile_page.png)

1. Press the left arrow button(go back) on the browser and the browser will navigate back to fetch data and the data loads correctly. 

    ![Verify every links](_images/ClientBlazorWithIndAuth/Go_back.png)

1. Press the logout button and you will log out.

    ![Verify every links](_images/ClientBlazorWithIndAuth/Logout_F5.png)


### Publish to Azure

1. Right-click Server > Publish, choose Azure > Azure App Service(Windows) > Next.

    ![Verify every links](_images/ClientBlazorWithIndAuth/Publish_page.png)

1. Sign in your account, select "WTE" in the "Subscription" dropdown.

1. In the upper right corner of the publish dialog, click the plus to create a new Azure application service.
    
    ![Create new web app](_images/SimpleWebAppWithClientSideBlazor/Create-new-appservice.png)

1. Create a new web app in an existing or new Resource Group / Hosting Plan, click Create.

    ![Create new web app](_images/ClientBlazorWithIndAuth/Publish_page2.png)
    
1. After profile creation, it will automatically add a database configuration dependency under the "Service Dependencies" node.

    - There is a warning about "Dependency mssql1" is by design according to [bug 109857](https://devdiv.visualstudio.com/DevDiv/_workitems/edit/1098574)

    ![Create new web app](_images/ClientBlazorWithIndAuth/Publish_page3.png)

1. Click Configure > Select "Azure SQL Database" > Select an existing or new database, then click next > Fill in corresponding strings to the specific textboxs, then click "Finish" button to add database.

    ![Create new database](_images/ClientBlazorWithIndAuth/configuration_database.png)

1. Click Edit in Publish Summary panel > Settings, check "Use this connection string at runtime" under Databases and "Apply this migration on publish" under Entity Framework Migrations, then click Save.

    ![Create new web app](_images/ClientBlazorWithIndAuth/Publish_edit.png)

1. Open appsettings.json under the server project and add the following fragment inside the "IdentityServer" configuration.
    
    ```
    "Key": {
        "Type": "Development"
    }
    ```

    ![Create new web app](_images/ClientBlazorWithIndAuth/Add_key.png)

1. Click Publish button to publish the application to Azure, verify that the application runs fine on the published site.

    - The browser should be openned automatically and show the same page as run on the published site.
       - **Note:** If you meet "HTTP Error 500.31 - ANCM Failed to Find Native Dependencies", please navigate to https://aspnetcoreon.azurewebsites.net/ to compare the SDK version you are using.
        - If it's a preview release or a   GA release sdk, do SCD as a workaround to publish successfully. When this sdk is released and runtime on azure is available, publish with FDD with installing runtime extension on the portal should work.
        - Workaround: Click "show all settings", navigate to Setting tab, set the **Deployment Mode** to **Self-Contained**.
        
    ![Create new web app](_images/ClientBlazorWithIndAuth/Self_Contained.png)

1.  On the browser page, try to perform the same steps as run and verify that it works well in each step. 

    ![Create new web app](_images/ClientBlazorWithIndAuth/Publish.png)

    **NOTE**: Remember to clean up the created web app or resource group if the test was completed successfully.