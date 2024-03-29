The package is a zero-dependency module that loads environment variables from files whose name start with `.env`:

- `.env.[process.env.NODE_ENV].local`
- `.env.local`
- `.env.[process.env.NODE_ENV]`
- `.env`

The package will read these files, parse data with variable / value, then put into `process.env`.

Same variable's name between diferent `.env` files will take precedence: `.env.[process.env.NODE_ENV].local` > `.env.local` > `.env.[process.env.NODE_ENV]` > `.env`. For Example:

in `.env.production.local`

```
DB_SECRET=1234
```

in `.env.local`

```
DB_SECRET=abc
```

`DB_SECRETE=1234` will work.

#### How it work

Let's say that you have set `process.env.NODE_ENV = "development"`, and then this package will read `.env.development.local`, `.env.local`, `.env.development`, `.env` one by one, ingore files which not exist, parse every line to key/value, join into one map, and put into `process.env`.

#### Install

```shell
$ npm install -i @btboy/dotenv
```

#### Usage

```js
import initEnv from "@btboy/dotenv";

initEnv({});
```

#### Options

##### cwd

Default: `process.cwd()`

You may specify a custom path your `.env` files. the module will find them here.

```
initEnv({cwd: process.cwd()});
```

##### Debug

Default: `false`

You may turn on logging to help debug why certain keys or values are not being set as you expect.

```
initEnv({Debug: true });
```

##### encoding

Default: `utf8`
You may specify the encoding of your file containing environment variables.

```
initEnv({encoding: `utf8` });
```
