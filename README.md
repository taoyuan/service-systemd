# service-systemd

[![NPM Version](http://img.shields.io/npm/v/service-systemd.svg?style=flat)](https://www.npmjs.org/package/service-systemd)
[![NPM Downloads](https://img.shields.io/npm/dm/service-systemd.svg?style=flat)](https://www.npmjs.org/package/service-systemd)

[![NPM](https://nodei.co/npm-dl/service-systemd.png)](https://nodei.co/npm/service-systemd/)

[![JS Standard Style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

Setup node.js app as systemd service, so can do 

```
$ sudo service my-node-service start | stop | restart
```

## Installing

```
$ npm i -g service-systemd
```

### Quick start

- Install service

  + pass settings in command line
  ````bash
  $ sudo service-systemd -a -n my-service -c /path/to/service -A main.js
  ````

  + pass all settings in JSON file
  ````bash
  $ sudo service-systemd -a -s service.json
  ````

- Uninstall service

````bash
$ sudo service-systemd -r -n myservice
````

## Using as module

````js
const service = require('service-systemd')

// add service

service.add({
  name: 'my-node-service',
  cwd: '/path/to/app',
  app: 'main.js',
  env: {
    PORT: 3002,
  }
})
.then(() => {
  console.log('my-node-service installed')
})
.catch((err) => {
  console.error('something wrong', err.toString())
})

// remove service

service.remove('my-node-service')
.then(() => {
  console.log('my-node-service removed')
})
.catch((err) => {
  console.error('something wrong', err.toString())
})

````

## Documentation

See [documentation](./doc/README.md) for further informations.

## Changelog

v. 3.1.0

- Add support for module use

v. 3.0.0

- All settings can be passed by command line
- Settings can have pseudo-template string like {ervice} or {engine} es. engine.bin
- Renamed binary form ``service-systemd`` to ``service-systemd``
- Renamed settings from ``wrap`` to ``engine``
- Renamed settings from ``path`` to ``cwd``
- Renamed settings from ``script`` to ``app``
- Added settings: ``author``, ``engine.args``
- Use ``logrotate`` settings on ``node`` and ``forever`` engines

## TODO

- test tdd
- jsdoc documentation
- test bdd
- rollback on error during ``add``
- run multiple instances
- check input settings usign ``checkv``
- add support for ``crontab`` dependents scripts
- check ``systemd`` on board
- add ``pm2`` as engine option
- setup ``nginx`` configuration adding new site (add nginx settings)

---

### Thanks to

[Chris Lea](https://github.com/chrislea) for these articles
- https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-1
- https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-2

Similar package  
- [strong-service-systemd](https://github.com/strongloop/strong-service-systemd)

References  
- https://www.freedesktop.org/software/systemd/man/systemd.exec.html


## License

The MIT License (MIT)

Copyright (c) 2017, [braces lab](https://braceslab.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
