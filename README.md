
Senegalhistory
==============

![Texte alternatif](http://farm4.staticflickr.com/3732/9952787965_d32eb66f3e_b_d.jpg "texte pour le titre, facultatif")

Senegalhistory is an open source project initiated by Open Knowlege Foundation Local Initiative which aims to to
track events marking the history of senegal
history of the resistors, the hostoriques monuments
the colonial and post-colonial era of senegal by giving more
possible details.

Senegalhistory is an open source tool based on https://github.com/okfn/timemapper with a few local touches.



Create beautiful timelines and timemaps from Google Spreadsheets.

Built by members of [Open Knowledge Foundation Labs](http://okfnlabs.org/).

See it in action at <http://timemapper.okfnlabs.org/>

# Install

## Local Install

This is a Node web-app built using express.

Install Node (>=0.8 suggested) and npm then checkout the code:

    git clone https://github.com/okfn/hypernotes

Then install the dependencies:

    cd hypernotes
    npm install . 
    # for some vendor modules
    git submodule init && gitsubmodule update

Finally, you may wish to set configuration options such as database name, port
to run on etc. To do this:

    # copy the settings.json template to settings.json
    cp settings.json.tmpl settings.json
    # then edit as necessary

Now you can run the app:

    node app.js

To view the site, open localhost:3000 in a browser.

### Configuration

The default configuration can be found in  `lib/config.js`. You can override
this in a couple of ways:

1. Create a `settings.json` with specific values. `settings.json` has the same
   form as nconf.defaults object in in `lib/config.js`.

2. Set specific environment variables. The ones you can set are those used in
   `nconf.defaults. This useful for deployment on Heroku where environment
   variables are default way to configure.

## Deploy (to Heroku)

Standard stuff:

    heroku create hypernotes
    git push heroku

You'll also need to set config. Suggest creating a `.env` file:

    TWITTER_KEY=...
    ...

Then push it:

    heroku config:push



# Overview for Developers

* NodeJS app but very frontend JS oriented
* Most of "presentation" including visualizations are almost entirely in frontend javascript
* Backend storage of "metadata" is onto s3 or local filesystem with storage of
  actual data (data for timelines/timemaps etc) into google docs spreadsheets

## Backend Storage

Layout follows frontend urls:

    /{username}/data.json                     # user info
    /{username}/{dataview}/datapackage.json   # config for the dataview
    /{username}/{dataview}/... other files    # (none atm but possibly we store data locally in future)

## Data View info

Stored in datapackage.json following [Data Package spec][dp-spec]. Key points:

* name, title, licenses etc as per [Data Package][dp-spec]
* info on google doc data source stored in first resources item in format compatible with [Recline][]:

        resources: [{
          backend: 'gdocs',
          url: 'gdocs url ...'
        }]

* additional config specific to timemapper in item call tmconfig. We will
  be gradually adding values here but at the moment have:

        tmconfig: {
          dayfirst: false     # are dates dayfirst
          layout: timemap     # timemap | map | timeline
          timelineJSOptions:  # options to pass to timelinejs
        }

[dp-spec]: http://data.okfn.org/standards/data-package
[Recline]: http://okfnlabs.org/recline/



# User Stories

Alice: user, who wants to create timelines, timemaps etc
Bob: visitor (and potential user)
Charlie: Admin of the website


## Register / Login

[ip] As Alice I want to signup (using Twitter?) so that I have an account and can login

As Alice I want to login (using Twitter?) so that I am identified to the system and the Vizs I create are owned by me

As Alice I want to see a terms of service when I signup so that I know what the licensing arrangements are for what I create and do

## Create and Edit Views

As Alice I want to create a timemap Viz quickly from a google spreadsheet ...
  - I want to set the title and "slug" for my timemap and have a nice url /alice/{name-of-viz}
  - I want to choose a license (or full copyright) - default license applied. Licenses will be open licenses or full copyright.
  - I want to create an animated timemap in which the time and map interact ...
  - I want to add a description (and attribution) to my Viz (perhaps now or later ...)

As Alice I want to edit my Viz later after I've created it (e.g. change the title) so that I can correct typos or update info to reflect changes

As Alice I want to create a timeline Viz quickly from my google spreadsheet so that I can share it with others

As Alice I want to create a timemap / timeline quickly from a gist so that I can share it with others
  - Structure of gist??

As Alice I want to create a map quickly from a google spreadsheet ...

As Alice or Bob I want to embed my Viz in a website elsewhere so that people can see it there

As Alice I want to watch a short (video) tutorial introducing me to how this works so that I have help getting started

As Alice or Bob I want to create a Viz without logging in so that I can try out the system without signing up
  - Is this necessary if sign up is really easy?

## Forking

I want to "fork" someone elses visualization so that I can modify and extend it

## Listing and Admin

[x] As Alice I want to list the "Vizs (viz?)" I've created 

[ip] As Bob I want to know what I can do with this service before I sign up so that I know whether it is worth doing so
  - Some featured timemaps ...

[x] As Bob I want to see all the Vizs created by Alice so that I can see if there some I like

  - Most recent items ?

As Bob I want to see recent activity by Alice to get a sense of the cool stuff she has been doing so that I know to look at that stuff first

As Alice I want to delete a Viz so that it is not available anymore (because I don't want it visible)

As Alice I want to undo deletiion of a Viz that I accidentally deleted so that it is available again

As Alice I want to revert to previous versions of my Viz so that I can see what it was like before

As Alice I want to "hide" a Viz so that it is not visible to others (but is visible to me)
  - Is this hidden in the listing or more than that? What about people who already have the url

As Charlie I want to be able to delete someone's Viz (or account) so that it no longer is available (because they want it down or someone else does etc)

## Access Control

As Alice I want to allow a Viz built on a private spreadsheet in google docs so that I don't have to make that spreadsheet public to create a Viz of it

As Alice I want to restrict access to some of my Vizs so that only I can see them

As Alice I want to restrict access to some of my Vizs but allow specific other people to view it so that other people than me can see it

## Misc

As Bob I want to find out about the website and project so that I get a sense of who's behind it / whether its trustworthy / whether there is other cool stuff they do

As Alice I want to know how many people have viewed my Viz so that I know whether other people are interested

As Bob (? may need to be logged in) I want to "star" a Viz I come across so that I recognize its value and store it for finding later

## Asides

- config
  - layout of the map / timeline (stacked versus side by side)
  - date parsing
- 2 types of data source - gists as well as google docs
  - data package structure in gists!

# History

First version was Microfacts / Weaving History <http://weavinghistory.org>

