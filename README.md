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

### For use

As an end user
(i.e., someone who just wants to use this tool,
not modify it),
the easiest way to install it is with [pipx].
First, [install pipx],
and confirm you can successfully invoke it:

    pipx --version

Then use it to install this tool:

    pipx install git+https://github.com/MrDOS/bna-scraper.git

[pipx]: https://pipx.pypa.io/stable/
[install pipx]: https://pipx.pypa.io/stable/how-to/install-pipx/

### For development

If you want to hack on the tool itself,
make a local clone of the repository:

    git clone https://github.com/MrDOS/bna-scraper.git

Then create a [virtual environment] – a “venv” – inside the source directory,
activate it (so that Python tools like pip work within it instead of globally),
and [editably install] the tool into that venv:

    cd bna-scraper/
    python3 -m venv .venv
    . .venv/bin/activate
    pip install --editable .

You'll need to re-activate the venv
every time you want to use the tool.

[virtual environment]: https://docs.python.org/3/tutorial/venv.html
[editably install]: https://setuptools.pypa.io/en/latest/userguide/development_mode.html

## Using

When run with the `--help` argument,
the script will tell you about its supported arguments and options:

    scrape-bna --help

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

    scrape-bna \
        --session 'BivH+fhT...' \
        "https://www.britishnewspaperarchive.co.uk/viewer/bl/..."

Note that the Windows `cmd.exe` shell
does not use single quotation marks (`'`)
to quote arguments like \*nix shells do.
You must either not quote the URL
or quote it in double quotes,
regardless of what any errant software developer
might tell you!
