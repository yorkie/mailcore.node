
mailcore.node
=============

MailCore provide a simple API to work with e-mail protocols IMAP, POP and SMTP on NodeJS


### Installation

```sh
$ npm install mailcore --save
```

### Usage

```js
var imap = new IMAPSession(993, 'imap.gmail.com', {
  secure: 'ssl',
  auth: {
    username: 'yorkiefixer@gmail.com',
    password: 'xxxxxxxxx'
  }
});

imap.connect();
imap.once('error', function(err) {
  throw err;
});
imap.once('connect', function() {
  console.log('connected');
  imap.select('INBOX', function(inbox) {
    console.log(inbox);
  });
  imap.fetchMessagesByNumber(0, 2, null, function(messages) {
    console.log(messages);
  });
});

```

If you want to get more details, you could go to [API.md](docs/API.md).

### TODO

* API `imap.seach`
* API `imap.fetchMessagesByNumber` and `imap.fetchMessagesByUID`
* API `imap.search`
* API `imap.appendMessage`
* API `imap.copyMessages`

### License

MIT