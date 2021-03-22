### 1. Provision a new hobby-basic database:

`heroku addons:create heroku-postgresql:hobby-basic -a YOUR_APP_NAME`

This will output a name for the new database containing a color. You will need to refer to this later. For example:

HEROKU_POSTGRESQL_PINK_URL

### 2. Optionally put db into maintenance mode to ensure that no data is added to the db while it's being copied.

`heroku maintenance:on --app YOUR_APP_NAME`

### 3. Copy the existing hobby-dev db to the hobby-basic db

`heroku pg:copy DATABASE_URL HEROKU_POSTGRESQL_PINK --app YOUR_APP_NAME`

Heroku will now print the following message.

heroku pg:copy DATABASE_URL HEROKU_POSTGRESQL_PINK --app YOUR_APP_NAME
```
!    WARNING: Destructive Action
!    Transfering data from DATABASE_URL to HEROKU_POSTGRESQL_PINK
!    This command will affect the app: YOUR_APP_NAME
!    To proceed, type "YOUR_APP_NAME" or re-run this command with --confirm YOUR_APP_NAME
```
YOUR_APP_NAME

### 4. Confirm db transfer by typing the actual name of your application

`YOUR_APP_NAME`

### 5. Promote your new database

`heroku pg:promote HEROKU_POSTGRESQL_PINK --app YOUR_APP_NAME`

The color-based name of the database you promote should be copied from the output you got up in step 1. Do not copy and paste the line above word for word, it will not work.

### 6. If you put your db into maintenance mode earlier, turn it off.

`heroku maintenance:off --app YOUR_APP_NAME`
