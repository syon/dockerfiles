puppeteer
=========

docker image for puppeteer.

- [puppeteer/troubleshooting\.md at master · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#running-puppeteer-in-docker)


## install

```bash
docker pull syon/puppeteer:latest
```


## example usage

__files__
```
.
├── Dockerfile
├── main.js
├── package.json
└── result
    ├── example.pdf
    └── example.png
```

__package.json__
```json
{
  "name": "pptr",
  "version": "1.0.0",
  "scripts": {
    "start": "node main.js"
  },
  "dependencies": {
    "puppeteer": "^0.10.2"
  }
}
```

__main.js__
```js
const puppeteer = require('puppeteer');

(async() => {
  const browser = await puppeteer.launch({
    args: [
      '--no-sandbox',
      '--disable-setuid-sandbox'
    ]
  });
  const page = await browser.newPage();
  await page.goto('https://example.com', { waitUntil: 'networkidle' });
  await page.screenshot({ path: '/result/example.png' });
  await page.pdf({ path: '/result/example.pdf' });
  browser.close();
})();
```

__Dockerfile__
```dockerfile
FROM syon/puppeteer:latest

WORKDIR /work
COPY . /work

RUN npm install --silent

CMD ["npm", "start"]
```

__bash__
```bash
$ docker build -t pptr .

$ docker run --rm -v $(pwd)/result:/result pptr
```
