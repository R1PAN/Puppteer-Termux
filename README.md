# Puppteer-Termux
## copy ##
```
yes | pkg update
yes | pkg install git
git clone https://github.com/R1PAN/Puppteer-Termux
cd Puppteer-Termux
unzip *zip
yes | pkg install x11-repo
yes | pkg install tur-repo
yes | pkg install chromium
yes | pkg install nodejs
```
#
`````
const puppeteer = require('puppeteer-core');
const fs = require('fs');

screenshot('https://google.com').then(() => console.log('screenshot saved'));

async function screenshot(url) {
  const browser = await puppeteer.launch({
    headless: false,
    args: [
      "--no-sandbox",
      "--disable-gpu",
    ]
  });

  const page = await browser.newPage();
  await page.setViewport({width: 1920, height: 1080});
  await page.goto(url, {
    timeout: 0,
    waitUntil: 'networkidle0',
  });
  const screenData = await page.screenshot({encoding: 'binary', type: 'jpeg', quality: 100});
  if (!!screenData) {
    fs.writeFileSync('screenshot.jpg', screenData);
  } else {
    throw Error('Unable to take screenshot');
  }

  await page.close();
  await browser.close();
}
````

<img src="https://github.com/R1PAN/Puppteer-Termux/blob/r/screenshot.jpg" alt="Alt text" width="300" height="200">
