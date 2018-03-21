# Install puppeteer on MAC OS
`sudo npm install --save puppeteer --unsafe-perm=true`

# Print a PDF

```js
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('URL');
  await page.pdf({path: 'FILENAME.pdf', format: 'A4'});
  await browser.close();
})();

```
