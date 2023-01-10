## My Favorites

<img width="717" alt="image" src="https://user-images.githubusercontent.com/94133633/211009835-090cceff-4eb9-41c7-ab1e-aea17a4415e8.png">

If the user clicks on the plus button, the app is added to the favorites. The plus button changes to a checkmark button. If the user clicks on the checkmark button again, the app is deleted from the favorites and the plus button appears again.


#### Functionality


The App favourite function is offered in the app marketplace to highlight an app easily and ensure that I as an user can quickly find the app again.

To use the function, the user can click on the plus button inside the app card. As soon as this is done, the app is added to the favorites. The plus button changes to a checkmark button. If the user clicks on the checkmark button again, the app is deleted from the favorites and the plus button appears again.



Inside the DB this information will get stored - the portal db will know which user has which favorite selected and can easily retrieve the information for the Front-End
<br>

```diff
! GET: /api/apps/favourites
```

<br>
<br>

## App Overview

The app marketplace is providing a list of software applications of catena-x approved app providers.

Beside the generic list, apps can get viewed in specific pre-configured views
* List View
* Category (Use Case) View
additionally user can select app details to display additional information for a specific selected app and mark apps as favorite (Details about Favorites)

<img width="578" alt="image" src="https://user-images.githubusercontent.com/94133633/211010432-f2c31fe6-11d5-43bb-a495-b2a6e0ba237a.png">
 

#### Sub-Headlines


API is used to display the active apps of the CX network based on the released apps. If an app is under review or creation, the app wont show up in this view.
<br>

```diff
! GET: /api/apps/active
```

<br>
<br>

## App Details

The app details page is getting triggered/open from the app marketplace. When the user is clicking on the "Details" button of an app, the app details will get displayed.

Inside the app deatils following information will be stored

* app provider & name
* app supported language
* app description
* app images
* app documents
* subscription status

<img width="324" alt="image" src="https://user-images.githubusercontent.com/94133633/211010698-64636fd7-aa49-4cc2-b9e4-34b544cda738.png">


#### Sub-Headlines


The api is responding with all app details for a specific app id. Within the path, the app id is getting send. Additionally language can get set as optional parameter. If no value is send for "language" inside the request call, english will be used as default language setting for the app detail response.   
Additionally the app subscription status is included.
<br>

```diff
! GET /api/apps/{appId}
```

Subscription Status Management:
The "Subscribe" button shows different state and color depending on the company subscription status. Below the button states are shown:

<img width="465" alt="image" src="https://user-images.githubusercontent.com/94133633/211010886-3c1be3e3-7796-4ea3-bc48-fc11fe42c4b0.png">

<br>
<br>

## My Business Applications

My Business Applications is a component inside the portal which shows the current logged in user which business applications the user can actively used.   
The logic is implemented based on

* company subscribed apps
* user roles

The component can hold up to 4 apps in one page, in case the user has more apps assigned, the component will turn to a carousel with the option to scroll through the pages.

<img width="512" alt="image" src="https://user-images.githubusercontent.com/94133633/211011143-07efa8a9-be1b-4392-897b-42adf90c2e02.png">

<br>

With a click on the business app tile, the user gets automatically redirected to the respective app and via SSO, the user can work inside the app.

<img width="715" alt="image" src="https://user-images.githubusercontent.com/94133633/211011399-00ab6584-2acf-4716-ad74-912bf85b0b7b.png">

The idp of the business application will check the user token. If the user token is valid, the user gets access to the respective tenant. If not, a permission / access error page is getting displayed.  
Important: to enable the functionality, an idp connection must be existing between the business app and catena-x.  
This connection is a user federation which establishes trust between the app idp and catena-x idp and enabled users with a valid key to access there subscribed app tenant.
 

#### Sub-Headlines

#### DB Details

Relevant DB tables

* company_user_assigned_roles
* user_roles
* app_assigned_clients
* company_assigned_offers


####  #1 Get my Business Applications
The API Backend call is retrieving all apps, where the current user is having an active role assigned.
The service call is getting triggered for an individual user as soon as this user logs in to the application.

Important for the function is an active company subscription of the assigned users company.
<br>

```diff
! GET: /api/apps/business
```

<br>
<br>



