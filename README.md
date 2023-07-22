# Grundo's Café stamp album helper

This is a userscript, you can install it with the Tampermonkey browser extension.

![Screenshot of a stamp album with the script activated](./screenshot.png)

Features:

- Fill blank album slots with images of what is missing
- Show name, rarity and description of missing stamps
- Links to searches (Wizard, TP, Auction) and Jellyneo
- Compare your album progress with another user

Credits:

Modelled after the userscript [Stamp album helper](https://www.reddit.com/r/neopets/comments/ldrb2d/userscript_stamp_album_helper_i_made_this_tool/) by [u/Eat_Wooloo_As_Mutton](https://www.reddit.com/user/Eat_Wooloo_As_Mutton/) which was made for retail neo.


### Developing the script

#### Adding a new stamp album
- Add a new entry to `stamps.json`
- Increment the minor version in `script.user.js`
- To get the stamp info for an album, you can seek out the information manually on Jellyneo or get some help with the script for the browser console below. 
1. Visit the [Jellyneo Item DB Page](https://items.jellyneo.net/search/?album=15&sort=6) for the album to get info on
2. Open the first stamp
3. Open a browser console (Ctrl + Shift + I in Firefox)
4. Paste the script below and Enter
5. Right click the array that is printed to the console and press 'Copy Object'
6. Paste it in stamps.json
7. Repeat for other stamps
8. Format stamps.json


```javascript
(function(){
  let name = document.querySelector('h1').textContent
  let rarity = parseInt(document.querySelector(`[class^='rarity-label']`).previousSibling.textContent.trim().split('r')[1])
  let description = document.querySelector("div > p > em").textContent
  let img = document.querySelector(`a[href*='images.neopets']`).href.split('/items/')[1]
  return [name,rarity,description,img]
})()
```

#### Preview a version of stamps.json
The script reads the URL for stamps.json from the localStorage key `stamp_database`. So you can upload your copy of stamps.json somewhere and set the localStorage key:
- `localStorage.setItem('stamp_database', YOUR_URL)`

Don't forget to clear it to use the default production URL again
- `localStorage.removeItem('stamp_database')`