mailcore.node
=============

MailCore provide a simple API to work with e-mail protocols IMAP, POP and SMTP on NodeJS


### Installation

```sh
$ npm install mailcore --save
```

### API

#### Class: IMAPSession

The IMAPSession class the class that can be implemented to handle the IMAP operators, like `LOGIN`, `FETCH`, `COPY` and etc, and this class inherits from `EventEmitter` indirectly, then you could use methods of `EventEmitter` to simplify your source code.

#### Event: 'error'

* err `Error` the error object

When an arbitrary error is raised, it will emit a 'error' event.

Because the trigger should be called once in one session, then use the best practice:

```js
imap.once('error', yourErrorHandler);
```

to avoid memroy leaks.

#### Event: 'connect'

When the account has been authenticated/loged in, it will emit a `connect` event.

Because the trigger should be called once in one session, then use the best practice:

```js
imap.once('connect', yourErrorHandler);
```

to avoid memroy leaks.

#### new IMAPSession(port, hostname, option)

* port Number, the port number of IMAP server
* hostname String, the hostname of IMAP server
* option Object, you config the authenticate option here

Constructs an instance of IMAPSession with these 3 specified arguments, and an simple example for calling this constructor just is following:

```js
var session = new IMAPSession(993, 'imap.gmail.com', {
  secure: 'ssl',
  auth: {
    username: 'yorkiefixer@gmail.com',
    password: 'xxxxxxx'
  }
});
```

As you have seen before, the secure has multiple values that you're able to pass, the below is the complete valided value for the `option.secure` field:

* ssl
* starttls
* none/null

The `option.auth` field before just use the plain to request the authentication, and if you want to use `XOAuth2`, then:

```js
{
	username: 'yorkiefixer@gmail.com',
	accessToken: 'your access_token'
}
```

(In later version, we can support the auto fetch the token when you specified `clientId`, `clientSecret` and `refreshToken`).

#### imap.connect([callback])

Start to create the connection to IMAP server, once you account has been authenticated/loged in, program would call `callback` and trigger the `connect` event.

#### imap.disconnect([callback])

End this session.

#### imap.select(folder, callback)

* folder String, the path of folder

Select a folder(mailbox).

#### imap.fetchMessagesByNumber(start, end, option, callback)
#### imap.fetchMessagesByUID(start, end, option, callback)

* start Number|String
* end Number|String
* option Number|Object|null TODO
* callback Function

Fetches the messages from you selected folder.

#### imap.search(query, callback)

* query String
* callback Function

The `SEARCH` command implementation.

#### imap.appendMessage(folder, data, flags, date, callback)

* folder String
* data String, rfc822 message data
* flags Array
* date Date
* callback Function

Append message to you specified folder.

#### imap.copyMessages(uids, dest, options, callback)

* uids Array, a uid set like: `[1000, 1001, 1003]`
* dest String, the folder that you want this message to
* options Object
* callback Function

Copy the messages that you specified by `uids` to `dest` folder.

### TODO

* API `imap.seach`
* API `imap.fetchMessagesByNumber` and `imap.fetchMessagesByUID`
* API `imap.search`
* API `imap.appendMessage`
* API `imap.copyMessages`

### License

MIT