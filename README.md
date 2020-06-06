<div style="text-align: center">
    <img src="https://github.com/cs01/termpair/raw/master/termpair/frontend_src/src/logo.png"/>
    <p>View and control remote terminals from your browser with end-to-end encryption</p>

</div>

**Documentation**: [https://cs01.github.io/termpair](https://cs01.github.io/termpair)

**Source Code**: [https://github.com/cs01/termpair](https://github.com/cs01/termpair)

**Try It**: [https://grassfedcode.com/termpair](https://grassfedcode.com/termpair)

## <a href="https://badge.fury.io/py/termpair"><img src="https://badge.fury.io/py/termpair.svg" alt="PyPI version" height="18"></a>

## What is TermPair?

TermPair lets developers securely share and control terminals in real time.

<div style="text-align: center">
   <a href="https://github.com/cs01/termpair/raw/master/termpair_browser.gif"> <img src="https://github.com/cs01/termpair/raw/master/termpair_browser.gif"/></a>
</div>

## Usage

Start the TermPair server, or use the one already running at [https://grassfedcode.com/termpair](https://grassfedcode.com/termpair).

```
>> termpair serve
INFO:     Started server process [15455]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8000 (Press CTRL+C to quit)
INFO:     ('127.0.0.1', 35470) - "WebSocket /connect_to_terminal" [accepted]
```

Then share your terminal by running:

```
>> termpair share --port 8000
--------------------------------------------------------------------------------
Running '/bin/bash' and sharing to 'http://localhost:8000/?terminal_id=b26903e19ffff2bc9ace60491e8200d5'.
Type 'exit' or close terminal to stop sharing.
--------------------------------------------------------------------------------
```

You can share that URL with whoever you want. Note that anyone that has it can view and possibly control your terminal.

The server multicasts terminal output to all browsers that connect to the session.

## Security

Termpair uses AES-GCM 128 bit end-to-end encryption for all terminal input and output.

### How it Works

Before termpair sends terminal output to the server, it encrypts it using a secret key so the server cannot read it. The server forwards that data to connected browsers. When the browsers receive the data, they use the secret key to decrypt and display the terminal output.

Likewise, when a browser sends input to the terminal, it is encrypted in the browser, forwarded from the server to the terminal, then decrypted in the terminal by termpair and written to the terminal's input. The secret key is generated by termpair and embedded in a [part of the url](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/hash) that is not sent to the server.


## Run With Latest Version

Use [pipx](https://github.com/pipxproject/pipx) to run the latest version without installing:

Serve:
```
>> pipx run termpair serve
```

Then share:
```
>> pipx run termpair share -b  # -b flag opens the browser automatically
```

## Installation

You can install using [pipx](https://github.com/pipxproject/pipx) or pip:

```
>> pipx install termpair
```

or

```
>> pip install termpair
```

## API

To view the command line API reference, run:

```
>> termpair --help
```

## System Requirements

Python: 3.6+

Operating System:

- To view/control from the browser: All operating systems are supported.
- To run the server, `termpair serve`: Tested on Linux. Should work on macOS. Might work on Windows.
- To share your terminal, `termpair share`: Tested on Linux. Should work on macOS. Probably doesn't work on Windows.