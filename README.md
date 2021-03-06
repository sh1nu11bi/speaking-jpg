# speaking-jpg
A simple tool to hide encrypted text messages inside jpeg images.

## Why?
I stumbled upon [a comment on Hackernews](https://news.ycombinator.com/item?id=14825675) the other day. A secure messaging app that used Tor just passed a security audit and the commenter argued that while this would be safe, once your phone is seized by authorities your use of Tor for messaging would stick out like a sore thumb.

So why not use something way less conspicuous? Speaking-jpg allows you to embed messages in normal jpeg images that can be uploaded and shared via email or social media. Only if the counterparty knows that a message is contained AND has the same key they can retrieve and decrypt the message.

## Installation:

```
npm install speaking-jpg -g
```

## Usage
Embed a message into a jpg

```shell
speaking-jpg create
    --in=path/to/img.jpg
    --out=path/to/manipulatedimg.jpg
    --msg="message you want to embed"
    --key="encryptionpassword"
```

Read a message from a jpg

```shell
speaking-jpg read
    --in=path/to/img.jpg
    --key="encryptionpassword"
```

## Limitations
- Max message length is 65.000 bytes
- Image processing (e.g. resizing upon upload) might strip out the comment.

## How does it work?
speaking jpg embeds a comment byte marker into the jpg's meta data section, followed by the total length and a random byte series to identify the comment as speaking-jpg one. Image viewers ignore this segment when parsing the file.

The message itself is stored as aes-256-ctr encrypted utf8 bytes.
