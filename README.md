ts-framework
============

[![Build Status](https://travis-ci.org/nxtep-io/ts-framework.svg?branch=master)](https://travis-ci.org/nxtep-io/ts-framework) &nbsp; [![Coverage Status](https://coveralls.io/repos/github/nxtep-io/ts-framework/badge.svg?branch=master)](https://coveralls.io/github/nxtep-io/ts-framework?branch=master)

A minimalistic framework for typescript based applications, with async/await and decorators support.


## Getting Started

### Release Candidate Disclaimer

The current API is considered to be a "Release Candidate". That means that small, potentially breaking 
changes may still occur. Be sure to use a specific GIT_REV_HASH and a lock file in your project, so you
won't be immediately affected by such a change.

For example:

```bash
# Install using Yarn
yarn add git+https://github.com/nxtep-io/ts-framework.git#GIT_REV_HASH 

# Install using NPM
npm install --save git+https://github.com/nxtep-io/ts-framework.git#GIT_REV_HASH 
``` 

### TL;DR - A single file server

Configure a new Server instance and start listening on desired port. 

```typescript
import Server, { Logger, BaseRequest, BaseResponse } from 'ts-framework';

// Define a sample hello world route
const SampleRoutes {
  '/': async (req: BaseRequest, res: BaseResponse) => {
    res.success({ message: 'Hello world!' });
  }
}

// Define the server configuration
const server = new Server({
  port: process.env.PORT as any || 3000,
  routes: {
    get: SampleRoutes,
  },
});


// Startup the simple server
server.listen()
  .then(() => Logger.info(`Server listening on port: ${server.config.port}`))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

You can also check a full project seed in the [Examples directory](./example) of this repository.

### Usage Guide

Follow the [Usage Guide](./GUIDE.md) for the basic boilerplate and a sample project configuration with
Database and user authentication samples.

Internal components:

- Logger (backed by [winston](https://npmjs.org/package/winston))
- Database (backed by [Mongoose](https://npmjs.org/package/mongoose))
- Router (backed by [Express](https://npmjs.org/package/express))
  - **Controllers:** Classes for handling API calls with decorators and async/await support
  - **Filters:** Middlewares for body validation, permission handling and other interception routines
  - **Responses:**: Simple wrappers over `res.status(code).json(result)` for success and error responses.

External components available as built-in middlewares: 

- OAuth 2.0 (express-oauth2-server)
- Sentry (RavenJS)
- CORS (express/cors)
- Multipart (express/multer)
- User Agent (express-useragent and request-ip)
- Body Parser (express/body-parser)
- Method Override (express/method-override)
- Cookie Parser (express/cookie-parser)

Other external plugins and middlewares for this framework

- **[ts-framework-versioning](https://github.com/nxtep-io/ts-framework-versioning)**

    Handles API versioning using HTTP Headers.
    
- **[ts-framework-notification](https://github.com/nxtep-io/ts-framework-notification)**

    Handles transactional notifications using SMTP (email templates) and Firebase Messaging (push notifications).

- **[ts-framework-migration](https://github.com/nxtep-io/ts-framework-migration)**

    Advanced usage plugin for handling Schema migrations safely within production environments.

- **[ts-framework-sockets](https://github.com/nxtep-io/ts-framework-sockets)**

    Socket.io layer over the TS-Framework. Currently in public alpha.

- **ts-framework-queue (coming soon)**

    Redis based task rotation queue services. Currently in closed alpha.

- **ts-framework-cache (coming soon)**

    Redis based cache services for performance. Currently in closed alpha.

- **[ts-framework-sql](https://github.com/nxtep-io/ts-framework-sql)**

    MySQL / Postgres database layer based on TypeORM. Currently in  alpha.


## Documentation

Checkout the rendered TS Docs in the official page: [https://nxtep-io.github.io/ts-framework/](https://nxtep-io.github.io/ts-framework/)

To generate the Typedoc reference of the available modules directly from source, run the following command:

```sh
yarn run docs
```

Then check the documentation at `./docs/index.html`.


## License

The project is licensed under the [MIT License](./LICENSE.md).
