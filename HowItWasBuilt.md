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

my password: Strapi123
