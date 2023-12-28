# Requires

- fastn build from [this PR](https://github.com/fastn-stack/fastn/pull/1612) or
  latest release once this PR is merged
  
- postgresql: auth related feature require a database. Only postgres is supported for now.

# Running Instructions

- setup `.env`. This file will be automatically loaded by `fastn`

```sh
cp .env.example .env
```

- To use google mail as SMTP server:

    - go to [myaccount.google.com](https://myaccount.google.com/)
    - search for "App Passwords"
    - create one and pass it to `FASTN_SMTP_PASSWORD` in your `.env` file
    - `FASTN_SMTP_USERNAME` will be your email account you used to create the "App Password"
    - `FASTN_SMTP_HOST`, in this case, will be `smtp.gmail.com`
    - `FASTN_SMTP_SENDER_EMAIL` use your email that you used to create the "App Password"
    - `FASTN_SMTP_SENDER_NAME` Your name
    - set `DEBUG=true` to actually send emails

- database requires an empty "public" schema which is created by postgres by default.

- (OPTIONAL) use docker to create a new postgres db:

```sh
docker run --name=multiauthdb -p 5432:5432 \
          -e POSTGRES_PASSWORD=passwd \
          -e POSTGRES_USER=fastn \
          -e POSTGRES_DB=authdb \
          -d postgres:14
```

The connection string for the above db would be:

```
postgresql://fastn:passwd@localhost:5432/multiauth
```

- run the following command in your terminal:

```sh
fastn serve
```
