## How it was built (2020)

#### PostgreSQL

[Install](https://www.codementor.io/@engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb)

```bash
brew install postgresql
postgresql --version
psql --version
```

Start

```bash
brew services start postgresql
brew services list
psql postgres
```

Show users

```bash
\du
```

Create user

```bash
CREATE ROLE username WITH LOGIN PASSWORD '123';
```

Change password

```bash
\password postgres
```

OR

```bash
ALTER USER username WITH ENCRYPTED PASSWORD '123';
```

Add permissions

```bash
ALTER ROLE username CREATEDB;
\q
```

Create DB

```bash
psql postgres -U username

CREATE DATABASE databasename;
GRANT ALL PRIVILEGES ON DATABASE databasename TO username;
```

OR use Utility

```bash
createdb databasename -U username
```

Connect to a DB

```bash
\connect databasename;
```

Show all DBs

```bash
\l;
```

Show tables from connected DB

```bash
\dt
```

#### Create project

```bash
yarn create strapi-app reactavancado-api
```

- Custom
- postgres
- database: databasename
- enter
- enter
- username: username
- password: 123
- N

```bash
cd reactavancado-api
yarn develop
```

Strapi admin:
my password: Strapi123

#### Strapi CKEditor

[Tutorial](https://strapi.io/documentation/v3.x/guides/registering-a-field-in-admin.html#setup)

because of heroku we installed it 2 times, but the default is inside the plugin

```bash
yarn strapi generate:plugin wysiwyg

yarn add @ckeditor/ckeditor5-react @ckeditor/ckeditor5-build-classic

cd plugins/wysiwyg
yarn add @ckeditor/ckeditor5-react @ckeditor/ckeditor5-build-classic
```

Create and paste content
`/plugins/wysiwyg/admin/src/components/MediaLib/index.js`

Create and paste content
`/plugins/wysiwyg/admin/src/components/Wysiwyg/index.js`

Create and paste content
`/plugins/wysiwyg/admin/src/components/CKEditor/index.js`

Replace code
`/plugins/wysiwyg/admin/index.js`

```bash
yarn build
```

#### Populate Strapi

- extract dump
- copy uploads to /public
- start postgres
- copy strapi.sql to /

```bash
psql -h 127.0.0.1 -U strapi -d strapi_db -W < strapi.sql
```

#### Create dump

[psql](https://www.postgresql.org/docs/current/app-psql.html)
[pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html)

- -c (clean, to clear tables)
- --if-exists (clear table if exists)
- --exclud-table=strapi_administrator (do not send my configs to other ursers)
- -h (host)
- -U (user)
- -d (database)
- -W (request password)
- '>' (local data to dump) / '<' (dump to local data)

```bash
pg_dump -c --if-exists --exclud-table=strapi_administrator -h 127.0.0.1 -U strapi -d strapi_db -W > strapi.sql
```

#### Deploy

[heroku](https://strapi.io/documentation/v3.x/deployment/heroku.html)

Dump
[heroku-postgres-import-export](https://devcenter.heroku.com/articles/heroku-postgres-import-export)

static files:
[cloudinary](https://cloudinary.com/)

Strapi Provider
_send all static files to cloudinary_
_example: when upload a image_

```bash
yarn add strapi-provider-upload-cloudinary
```

create file: `/config/env/production/plugins.js`
paste configs from strapi-provider-upload-cloudinary

```bash
git commit -am"provider cloudinary"
git push heroku master
```

```bash
heroku config:set CLOUDINARY_NAME=my_value
heroku config:set CLOUDINARY_KEY=my_value
heroku config:set CLOUDINARY_SECRET=my_value
```

Webhook

- create file `/config/env/production/custom.js` and past content
- edit file `/api/landing-page/models/landing-page.js` and past content
