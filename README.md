# SPDY Server for node.js

With this module you can create [SPDY](http://www.chromium.org/spdy) servers
in node.js with natural http module interface and fallback to regular https
(for browsers that doesn't support SPDY yet).

It's using SSL's NPN feature that is available in node from 0.6.0 version, but
requires you to build node with latest openssl.

## Node+OpenSSL building

At the moment node-spdy requires zlib dictionary support, which will come to
node.js only in 0.7.x version. To build 0.7.x version with a bundled openssl
(that's needed for NPN feature) follow instructions below:

```bash
git clone git://github.com/joyent/node.git
cd node
./configure --prefix=$HOME/.node/dev # <- or any other dir

make install -j4 # in -jN, N is number of CPU cores on your machine

# Add node's bin to PATH env variable
echo 'export PATH=$HOME/.node/dev/bin:$PATH' >> ~/.bashrc

#
# You have working node 0.7.x + NPN now !!!
#
```

## Usage

```javascript
var spdy = require('spdy');

var options = {
  key: fs.readFileSync(__dirname + '/../keys/spdy-key.pem'),
  cert: fs.readFileSync(__dirname + '/../keys/spdy-cert.pem'),
  ca: fs.readFileSync(__dirname + '/../keys/spdy-csr.pem')
};

spdy.createServer(options, function(req, res) {
  res.writeHead(200);
  res.end('hello world!');
});

spdy.listen(443);
```

## Helping project

Node-spdy is open for donations, please feel free to contact me for any futher information: fedor@indutny.com

#### Contributors

* [Fedor Indutny](https://github.com/indutny)
* [Chris Storm](https://github.com/eee-c)
* [François de Metz](https://github.com/francois2metz)

#### LICENSE

This software is licensed under the MIT License.

Copyright Fedor Indutny, 2011.

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to permit
persons to whom the Software is furnished to do so, subject to the
following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN
NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM,
DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR
OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE
USE OR OTHER DEALINGS IN THE SOFTWARE.

