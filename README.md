# Workchat Google Calendar Plugin (ALPHA)

A google calendar plugin for Workchat client which allows you to create, delete, and get notifications from your google calendar events.

## Features
- Create events
- Delete Events
- Get 10 minute notifications
- Get event updates
- Status is set to Do Not Disturb when in a event (Manually required to reset it)
- Get invitations request within Workchat and reply to them instantly
- Get upcoming calendar events
- Get a summary for any day you like

## Build instructions
There is no built package available for installation, you need to compile the source code. This plugin cannot be installed on Workchat Cloud products, as Cloud only allows installing plugins from the marketplace.
1. Clone this repo.
2. Install [npm](https://www.npmjs.com/get-npm), [Golang](https://golang.org/doc/install), [golangci-lint](https://golangci-lint.run/usage/install/) and Automake.
3. Go into the cloned directory and run `make`. You will need to upload this to your workchat instance through the system console and provide it a Client secret and Client ID.
4. When building is finished, the plugin file is available at `dist/com.workchat.google-calendar-VERSION.tar.gz`
5. In your Workchat, go to **System Console** > **Plugin Management** and upload the `.tar.gz` file.

## Configure Google Calendar

1. Go to [Google Cloud Dashboard](https://console.cloud.google.com/home/dashboard) and create a new project.
2. After creating a project click on `Go to APIs overview` card from the dashboard which will take you to the API dashboard.
3. From the left menu select `Library` and activate the Google Calendar API.
4. From the left menu select `Domain verification` and verify the domain of your Workchat installation.
5. From the left menu select `Credentials`.
6. Now click on `Create Credentials` dropdown and select `OAuth client ID` option.
7. While creating the Oauth credentials, enter the values of `Authorized Javascript Origins` as `<Workchat server URL>` and the value of `Authorised redirect URIs` as `<Workchat server URL>/plugins/com.workchat.google-calendar/oauth/complete`.
8. After creating the Oauth client, copy the Client ID and secret.
9. Upload the plugin to Workchat and go to `Google Calendar Plugin settings`. Paste the client id and secret.
10. Enable the plugin and you should be able to see event reminder notifications.

## Installing For Development
You will be required to follow the above steps to acquire a Client ID and Client secret. 

1. Clone the repo and make sure `workchat server` and `workchat webapp` is up and running.
2. Use `ngrok` or any other tunnel provider to expose the workchat server port (8065) to Internet. The command to create a tunnel is `ngrok http 8065`. (Note: Google will need you to verify the domain. You can setup use Python SimpleHTTPWebServer to set one up and upload the file google provides to verify the domain.
Afterwards, you can close SimpleHTTPWebServer and run your Workchat Server)
3. Replace all instances of `*config.ServiceSettings.SiteURL` with your `ngrok` URL
4. Login to [Google Cloud Console](https://console.cloud.google.com) and create a new project.
5. Go to [API library](https://console.cloud.google.com/apis/library) and make sure Google Calendar API is enabled.
6. Go to [API and Services](https://console.cloud.google.com/apis/dashboard) and select `Credentials` tab from the left menu.
7. Now click on `Create Credentials` dropdown and select `Oauth client ID` option.
8. While creating the Oauth credentials, enter the values of `Authorized Javascript Origins` as `http://localhost:8065` and the value of `Authorised redirect URIs` as `http://localhost:8065/plugins/com.workchat.google-calendar/oauth/complete`.
9. After creating the Oauth client, copy the Client ID and secret.
10. Upload the plugin to Workchat and go to `Google Calendar Plugin settings`. Paste the client id and secret.
11. Enable the plugin and you should be able to see event reminder notifications.


## Contributing

If you are interested in contributing, please fork this repo and create a pull request!

## To-Do's / Future Improvements
- Change response to event within workchat
- Show conflicts when invited to event with other events on your calendar
- Better error logging / handling
- Optimizations in cron jobs for reminding users about 10 minutes until event as well as user in event
- Code refactoring
- More commenting throughout code to explain what's going on
- Set the calendar user wants to sync with (Currently it uses primary calendar)
- Customize reminder time (user can set if they want anything other than 10 minutes)
- Include a web app portion which displays the events for a particular day without user needing to enter commands
