# BNA Scraper

[The British Newspaper Archive][bna] only lets you download individual pages
of publications,
and even then only as low-resolution PDFs.
This script retrieves high-resolution original images
of individual pages,
ranges of pages,
or entire issues
based on the URLs provided by the API.

[bna]: https://www.britishnewspaperarchive.co.uk/

## Installing

This script requires Python 3.9.
Make sure you have a high enough version of Python installed:

    python3 --version

The only external dependency is [Requests].
This is a very popular library,
and may be packaged by your OS vendor.
For example, on Debian-based Linux distributions
(e.g., Debian, Ubuntu, Mint),
it's packaged as `python3-requests`:

    sudo apt install python3-requests

If all else fails, you can install it via pip:

    pip3 install requests

[requests]: https://pypi.org/project/requests/

## Using

When run with the `--help` argument,
the script will tell you about its supported arguments and options.
In POSIX-like shells:

    ./scrape --help

Or on Windows:

    python3 scrape --help

This script doesn't know how to log into the BNA website,
so you'll need to do so on its behalf.
You'll need to log into the website in your browser,
then pass the value of your login session cookie –
`session_0` –
to the script.

In Firefox:

1. Log into https://www.britishnewspaperarchive.co.uk/.
2. Open the web developer tools: from the Tools menu, open the Browser Tools submenu, and select “Web Developer Tools”.
3. Open the “Storage” tab of the web developer tools.
4. On the left-side navigation tree, expand “Cookies”, and select “https://www.britishnewspaperarchive.co.uk”.
5. In the table of cookies, locate the row with the name `session_0`. Double-click on the “Value” cell of that row, then right-click → copy the value.

In Chrome:

1. Log into https://www.britishnewspaperarchive.co.uk/.
2. Open the developer tools: from the View menu, open the Developer submenu, and select “Developer Tools”.
3. Open the “Application” tab of the developer tools.
4. On the left-side navigation tree, expand “Cookies”, and select “https://www.britishnewspaperarchive.co.uk”.
5. In the table of cookies, click on the row with the name `session_0`. In the “Cookie Value” pane below the table, select the cookie value, then right-click → copy it.

Pass this value to the `--session` flag:

    ./scrape \
        --session 'BivH+fhT...' \
        'https://www.britishnewspaperarchive.co.uk/viewer/bl/...'
