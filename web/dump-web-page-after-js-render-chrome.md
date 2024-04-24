# Dump web page after JavaScript rendering with Chrome

```
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --headless --incognito --dump-dom https://github.com > /tmp/github.html
```

Results in a single HTML file after the JavaScript has been executed. 
Includes images too.

Source: [A HN comment](https://news.ycombinator.com/item?id=39811223).

