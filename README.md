[![RIDLEY](https://telegra.ph/file/7a38dc0650b11ceced3b1.png)](https://youtu.be/Pk_TthHfLeE)

# Features supported:
- Mirroring direct download links to google drive
- Download progress
- Upload progress
- Download/upload speeds and ETAs
- Docker support
- Uploading To Team Drives.
- Index Link support
- Service account support
- Mirror telegram files

# How to deploy?
Deploying is lengthy process required patience & here goes the steps :

- Clone this repo in your device:
```
git clone https://github.com/Prashant-blip-cell/RIDLEY 
cd RIDLEY
```
- Install dependencies for running setup scripts:
```shell script
pip3 install -r requirements.txt
```

## Setting up config-sample file

- **BOT_TOKEN** : The telegram bot token that you get from @BotFather
- **GDRIVE_FOLDER_ID** : This is the folder ID of the Google Drive Folder/dir in which you want to upload all the mirrors.
- **TELEGRAPH_TOKEN** : The token generated by running:
```
python3 generate_telegraph_token.py
```
- **OWNER_ID** : The Telegram user ID.
- 
- **IS_TEAM_DRIVE** : (Optional field) Set to "True" if GDRIVE_FOLDER_ID is from a Team Drive else False or Leave it empty.
- 
- **INDEX_URL** : (Optional field) go here to generate your index url https://github.com/Achrou/goindex-theme-acrou
- 
- **API_KEY** : You can get this from https://my.telegram.org (DO NOT put this in quotes).
- **API_HASH** : You can get this from https://my.telegram.org
- 
- **USER_SESSION_STRING** : Session string generated by running:
```
python3 generate_string_session.py
```
Leave other fields as it is.

## Setting up config file by coping config-sample file to config file:
```
cp config_sample.env config.env
```
 
 
## Getting Google OAuth API credential file

- Visit the [Google Cloud Console](https://console.developers.google.com/apis/credentials)
- Go to the OAuth Consent tab, fill it, and save.
- Go to the Credentials tab and click Create Credentials -> OAuth Client ID
- Choose Desktop and Create.
- Use the download button to download your credentials.
- Move that file to the root of mirror-bot, and rename it to credentials.json
- Visit [Google API page](https://console.developers.google.com/apis/library)
- Search for Drive and enable it if it is disabled
- Finally, run the script to generate token file (token.pickle) for Google Drive:
```
pip3 install google-api-python-client google-auth-httplib2 google-auth-oauthlib
python3 generate_drive_token.py
```

## Deploying on Heroku using Termux:

- Install [Heroku cli](https://devcenter.heroku.com/articles/heroku-cli)
- Login into your heroku account with command:
```
heroku login
OR
heroku login -i
```
- Create a new heroku app:
```
heroku create <appname>
```
- Select This App in your Heroku-cli: 
```
heroku git:remote -a <appname>
```
- Change Dyno Stack to a Docker Container:
```
heroku stack:set container
```
- Add Heroku Postgres (only if you are deploying it for the 1st time)
```
heroku addons:create heroku-postgresql
```
- Add Private Credentials and Config Stuff:
```
git add -f credentials.json token.pickle config.env heroku.yml
```
- Commit new changes:
```
git commit -m "Added Creds."
```
- Push Code to Heroku:
```
git push heroku master --force
```
- Restart Worker by these commands,You can Do it manually too in heroku.
- For Turning off the Bot:
```
heroku ps:scale worker=0
```
- For Turning on the Bot:
```
heroku ps:scale worker=1	 	
```

## Youtube-dl authentication using .netrc file
For using your premium accounts in youtube-dl, edit the [.netrc](https://github.com/Prashant-blip-cell/RIDLEY/blob/master/.netrc) file according to following format:
```
machine host login username password my_youtube_password
```
where host is the name of extractor (eg. youtube, twitch). Multiple accounts of different hosts can be added each separated by a new line
