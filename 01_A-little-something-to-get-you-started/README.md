# A little something to get you started

## Solution

The CTF page source code contain a **background image** inside *style element* `background.png`.

```html

<!doctype html>
<html>
    <head>
        <style>
            body {
                background-image: url("background.png");
            }
        </style>
    </head>
    <body>
        <p>Welcome to level 0.  Enjoy your stay.</p>
    </body>
</html>
```

Visit the URL `https://YOUR-LAB-ID.ctf.hacker101.com/background.png` to retrive the flag. It should look something like this `^FLAG^YOUR-FLAG-ID$FLAG$`.
