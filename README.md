# jquery.remember
*a fork of [jquery.cookie](https://github.com/carhartl/jquery-cookie)*

Remember stuff. A simple way to set/read/destroy cookies and localstorage.

## Differences between $.cookie...

+ $.remember instead of $.cookie...
+ call using settings object. $.remember({ name: 'name', value: 'value' }) instead of params $.cookie('name', 'value')
+ sets localstorage first and falls back to cookies (browser capabilities). unless specified $.remember({ name: 'test', use: 'cookie' })
+ new options like get and set (if not set already...) $.remember({ name: 'name', value: 'value', getSet: true })
+ gets rid of amd settings from $.cookie (didn't work great for me). now you can include in require and whatever name as namespaced argument
+ complete code restructure
+ tried to preserve all of the features of $.cookie

## Installation

Include script *after* the jQuery library (unless you are packaging scripts somehow else -- minify at your convenience):
    
    <script src="/path/to/jquery.remember.js"></script>

## Usage

Create localstorage item (localstorage default, can be overwritten/specified)

    $.remember({ name: 'name', value: 'value' })

Create session cookie:

    $.remember({ name: 'name', value: 'value', use: 'cookie' });

Create expiring cookie lasting 20 years (adding cookie specific options -- expires/path/secure/domain -- forces cookie:

    $.remember({ name: 'name', value: 'value', expires: 365 * 20 });

Create localstore item (disallow cookie fallback):

    $.remember({ name: 'name', value: 'value', fallback: false });

Read (will automatically fallback + check the other for named pair, unless specified):

    $.remember({ name: 'name' });
    $.remember({ name: 'name', use: 'cookie', fallback: false });
    $.remember({ name: 'not_found' }) => null

Get or Set item:

    $.remember({ name: 'name', value: 'value', getSet: true }) => will not set if already exists

Remove cookie/localstorage:

    $.remember({ name: 'name', remove: true });
    $.remember({ name: 'name', use: 'localstorage', fallback: false });

## Configuration

### raw

By default the cookie/localstorage value is encoded/decoded when writing/reading, using `encodeURIComponent`/`decodeURIComponent`. Bypass this by raw to true:

    $.remember({ name: 'name', value: 'value', raw: true });

### json

Turn on automatic storage of JSON objects passed as the cookie value:

    $.remember({ name: 'name', value: 'value', json: true });


## Tests

Run over a server, example:

    $ python -m SimpleHTTPServer

Currently very basic test setup showing functionality, would be great to build this in actual testing framework (similar to $.cookie)

*If you prefer simple cookie management only, please check out the original repo at [jquery.cookie](https://github.com/carhartl/jquery-cookie)*
