        
    const server = http.createServer( (req, res) => {
      Promise.resolve({ req, res })
        .then(ctx => {
          
            ctx.res.writeHead(200, {'Content-Type': 'text/plain'});
            ctx.res.end('okay');
          
            return ctx;
        });
    });
    
## And the same with yeps:

    npm i -S yeps

app.js

    const App = require('yeps');
    
    const app = module.exports = new App();
    
    app.then(async ctx => {
      ctx.res.writeHead(200, {'Content-Type': 'text/plain'});
      ctx.res.end('Ok');
    });
    
    app.catch(async (err, ctx) => {
      ctx.res.writeHead(500);
      ctx.res.end(err.message);
    });

bin/www

    #!/usr/bin/env node
    
    const http = require('http');
    const app = require('../app');

    http
        .createServer(app.resolve())
        .listen(parseInt(process.env.PORT || '3000', 10));
    
package.json

    "scripts": {
      "start": "node bin/www"
    }
    
## Promise like middleware

By default all app steps will be finished. Except one of them has rejected promise:

    app.then(async ctx => {
      
      ctx.res.writeHead(200);
      ctx.res.end('test');
      
      return app.reject();
      
    }).then(async () => {
      
      // it wont work
    
    }).catch(async () => {
    
      // it wont work
    
    });
    
## Packages

* [Anatomy of an HTTP Transaction](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/) - node.js http server request documentation
* [yeps-promisify](https://github.com/evheniy/yeps-promisify) - YEPS kernel
* [yeps-benchmark](https://github.com/evheniy/yeps-benchmark) - performance comparison koa2, express and node http
* [yeps-router](https://github.com/evheniy/yeps-router) - YEPS promise based router
* [yeps-error](https://github.com/evheniy/yeps-error) - YEPS 404/500 error handler
* [yeps-redis](https://github.com/evheniy/yeps-redis) - YEPS promise based redis client - ioredis
* [yeps-logger](https://github.com/evheniy/yeps-logger) - YEPS Async logger - winston
* [yeps-boilerplate](https://github.com/evheniy/yeps-boilerplate) - YEPS app boilerplate
* [yeps-method-override](https://github.com/evheniy/yeps-method-override) - YEPS Method Override
* [yeps-bodyparser](https://github.com/evheniy/yeps-bodyparser) - YEPS body parser
* [yeps-cors](https://github.com/evheniy/yeps-cors) - YEPS Cross-Origin Resource Sharing (CORS)
* [yeps-mysql](https://github.com/evheniy/yeps-mysql) - YEPS Promise based mysql client
* [yeps-express-wrapper](https://github.com/evheniy/yeps-express-wrapper) - YEPS express wrapper
* [node-vagrant](https://github.com/evheniy/node-vagrant) - Node.js Vagrant config