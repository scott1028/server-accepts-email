# Server Accepts Email

Check if an SMTP server accepts emails to a given address.

## Installation

```sh
npm install --save server-accepts-email
```

## Usage

```js
const serverAcceptsEmail = require('server-accepts-email')

console.log(await serverAcceptsEmail('linus@folkdatorn.se'))
//=> true

console.log(await serverAcceptsEmail('6bJ4zsZHOE@folkdatorn.se'))
//=> false

console.log(await serverAcceptsEmail('linus@gp5uzpn2q7.se'))
//=> false
```

## API

### `serverAcceptsEmail(email[, options]) => Promise<boolean>`

- `email` (string, required) - Email address to test
- `options` (object, optional)
  - `senderDomain` (string, optional) - Domain to identify as (in `HELO` smtp command)
  - `senderAddress` (string, optional) - Email address to identify as (in `MAIL FROM` command)

## Other libraries

There are some other libraries that does the same thing, but I found them to have some flaws which made me write this one.

&nbsp; | Promise API | Follows [RFC5321](https://tools.ietf.org/html/rfc5321) <sup>1</sup> | Proper Errors <sup>2</sup>
----- | ----- | ----- | -----
**`server-accepts-email`** | ✅ | ✅ | ✅
[`email-exists`](https://github.com/scippio/email-existence) | ✅ | ❌ | ❌
[`email-existence`](https://github.com/MarkTiedemann/email-exists) | ❌ | ❌ | ❌
[`email-verify`](https://github.com/bighappyworld/email-verify) | ❌ | ❌ | ✅

<sup>1</sup> None of the other libraies parsed the replies to support multiline replies, but instead relied on every reply comming in a chunk, accepting all data and searching for substrings, or something similar.

<sup>2</sup> Some of the other libraries rejects, or calls callback, with something other than an `Error` instance.