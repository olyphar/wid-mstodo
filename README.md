# mstodo
Widget for [smashing](https://github.com/Smashing/smashing) dashboard, accessing [Microsoft To Do](https://to-do.microsoft.com/).
Microsoft To Do is the successor of Wunderlist - migration of tasks is easy to handle, authentication became a bit more complex.

## Description
![](https://user-images.githubusercontent.com/61623490/75611344-076bbd00-5b1a-11ea-8d8c-cb47341f759c.png)
## Dependencies

Add the following to your Gemfile

    gem 'rest-client'
    gem 'json'

and run `bundle-install`

You will need an application registered at [Microsoft Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
I have created an "Application from personal account" which provides a client ID and client secret that you will both need later.

The application should receive the permissions for `Tasks.Read` and `Tasks.Read.Shared` for the applications Exchange and Microsoft Graph

## Setup

Put the files in the respective folders of your smashing project.

Create a new file `assets/config/msauth_settings.json` with the following content

    {"clientsecret":"<YOUR CLIENT SECRET>","clientid":"<YOUR CLIENT ID>"}
    
Once the widget is loading properly, it will display an alphanumeric code which needs to be entered at https://www.microsoft.com/devicelogin - followed by some requesting of access rights
Wait a bit and authentication should

## Open points

- At the moment the task folder is still hard coded in line 150 of the job, you would need to adapt this to your own folder id.
- The refresh token is currently stored in the root directory of your dashboard. Since this token should be considered sensitive, I will need to find better storage for persistence across reboots.
- Proper implementation of server side paging is still missing. By default the server provides ten tasks at once and provides an URL for calling the next ten tasks. I am manually asking for 500 tasks at the moment.
- There's still a lot of console output for debugging stuff...

## Disclaimer

I am no expert in ruby or even web technologies, my experience is solely in embedded programming. So many of the things in this widget might not be done in the smartest way. My main requirement is fulfilled: my tasks are shown on my dashboard. Hope this works for you, too. I am happy to hear about improvement possibilities, though.
