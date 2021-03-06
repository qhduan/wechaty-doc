<a id="contact"></a>

# Contact
All wechat contacts(friend) will be encapsulated as a Contact.
[Examples/Contact-Bot](https://github.com/Chatie/wechaty/blob/1523c5e02be46ebe2cc172a744b2fbe53351540e/examples/contact-bot.ts)

**Kind**: global class  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| id | <code>string</code> | Get Contact id. This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table) |


* [Contact](/api/contact)
    * _instance_
        * [.say(textOrContactOrFile)](#Contactsay) <code>Promise.&lt;void&gt;</code>
        * [.name()](#Contactname) <code>string</code>
        * [.alias(newAlias)](#Contactalias) <code>Promise.&lt;(null&#124;string&#124;void)&gt;</code>
        * [.friend()](#Contactfriend) <code>boolean</code> &#124; <code>null</code>
        * [.type()](#Contacttype) <code>ContactType.Unknown</code> &#124; <code>ContactType.Personal</code> &#124; <code>ContactType.Official</code>
        * [.gender()](#Contactgender) <code>ContactGender.Unknown</code> &#124; <code>ContactGender.Male</code> &#124; <code>ContactGender.Female</code>
        * [.province()](#Contactprovince) <code>string</code> &#124; <code>null</code>
        * [.city()](#Contactcity) <code>string</code> &#124; <code>null</code>
        * [.avatar()](#Contactavatar) <code>Promise.&lt;FileBox&gt;</code>
        * [.self()](#Contactself) <code>boolean</code>
    * _static_
        * [.load(id)](#Contactload) [<code>Contact</code>](/api/contact)
        * [.find(query)](#Contactfind) <code>Promise.&lt;(Contact&#124;null)&gt;</code>
        * [.findAll([queryArg])](#ContactfindAll) <code>Promise.&lt;Array.&lt;Contact&gt;&gt;</code>

<a id="contactsay"></a>

## contact.say(textOrContactOrFile)

**Return the type of**: <code>Promise.&lt;void&gt;</code>


> Tips:
This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table)

**Kind**: instance method of [<code>Contact</code>](/api/contact)  

| Param | Type | Description |
| --- | --- | --- |
| textOrContactOrFile | <code>string</code> &#124; [<code>Contact</code>](/api/contact) &#124; <code>FileBox</code> | send text, Contact, or file to contact. </br> You can use [FileBox](https://www.npmjs.com/package/file-box) to send file |

**Example**  
```js
const bot = new Wechaty()
await bot.start()
const contact = await bot.Contact.find({name: 'lijiarui'})  // change 'lijiarui' to any of your contact name in wechat

// 1. send text to contact

await contact.say('welcome to wechaty!')

// 2. send media file to contact

import { FileBox }  from 'file-box'
const fileBox1 = FileBox.fromUrl('https://chatie.io/wechaty/images/bot-qr-code.png')
const fileBox2 = FileBox.fromFile('/tmp/text.txt')
await contact.say(fileBox1)
await contact.say(fileBox2)

// 3. send contact card to contact

const contactCard = bot.Contact.load('contactId')
await contact.say(contactCard)
```
<a id="contactname"></a>

## contact.name()

**Return the type of**: <code>string</code>


Get the name from a contact

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
const name = contact.name()
```
<a id="contactalias"></a>

## contact.alias(newAlias)

**Return the type of**: <code>Promise.&lt;(null&#124;string&#124;void)&gt;</code>


GET / SET / DELETE the alias for a contact

Tests show it will failed if set alias too frequently(60 times in one minute).

**Kind**: instance method of [<code>Contact</code>](/api/contact)  

| Param | Type |
| --- | --- |
| newAlias | <code>none</code> &#124; <code>string</code> &#124; <code>null</code> | 

**Example** *( GET the alias for a contact, return {(Promise&lt;string | null&gt;)})*  
```js
const alias = await contact.alias()
if (alias === null) {
  console.log('You have not yet set any alias for contact ' + contact.name())
} else {
  console.log('You have already set an alias for contact ' + contact.name() + ':' + alias)
}
```
**Example** *(SET the alias for a contact)*  
```js
try {
  await contact.alias('lijiarui')
  console.log(`change ${contact.name()}'s alias successfully!`)
} catch (e) {
  console.log(`failed to change ${contact.name()} alias!`)
}
```
**Example** *(DELETE the alias for a contact)*  
```js
try {
  const oldAlias = await contact.alias(null)
  console.log(`delete ${contact.name()}'s alias successfully!`)
  console.log('old alias is ${oldAlias}`)
} catch (e) {
  console.log(`failed to delete ${contact.name()}'s alias!`)
}
```
<a id="contactfriend"></a>

## contact.friend()

**Return the type of**: <code>boolean</code> &#124; <code>null</code>


Check if contact is friend

> Tips:
This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table)

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Returns**: <code>boolean</code> &#124; <code>null</code> - <br>True for friend of the bot <br>
False for not friend of the bot, null for unknown.  
**Example**  
```js
const isFriend = contact.friend()
```
<a id="contacttype"></a>

## contact.type()

**Return the type of**: <code>ContactType.Unknown</code> &#124; <code>ContactType.Personal</code> &#124; <code>ContactType.Official</code>


Return the type of the Contact
> Tips: ContactType is enum here.</br>

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
const bot = new Wechaty()
await bot.start()
const isOfficial = contact.type() === bot.Contact.Type.Official
```
<a id="contactgender"></a>

## contact.gender()

**Return the type of**: <code>ContactGender.Unknown</code> &#124; <code>ContactGender.Male</code> &#124; <code>ContactGender.Female</code>


Contact gender
> Tips: ContactGender is enum here. </br>

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
const gender = contact.gender() === bot.Contact.Gender.Male
```
<a id="contactprovince"></a>

## contact.province()

**Return the type of**: <code>string</code> &#124; <code>null</code>


Get the region 'province' from a contact

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
const province = contact.province()
```
<a id="contactcity"></a>

## contact.city()

**Return the type of**: <code>string</code> &#124; <code>null</code>


Get the region 'city' from a contact

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
const city = contact.city()
```
<a id="contactavatar"></a>

## contact.avatar()

**Return the type of**: <code>Promise.&lt;FileBox&gt;</code>


Get avatar picture file stream

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Example**  
```js
// Save avatar to local file like `1-name.jpg`

const file = await contact.avatar()
const name = file.name
await file.toFile(name, true)
console.log(`Contact: ${contact.name()} with avatar file: ${name}`)
```
<a id="contactself"></a>

## contact.self()

**Return the type of**: <code>boolean</code>


Check if contact is self

**Kind**: instance method of [<code>Contact</code>](/api/contact)  
**Returns**: <code>boolean</code> - True for contact is self, False for contact is others  
**Example**  
```js
const isSelf = contact.self()
```
<a id="contactload"></a>

## Contact.load(id)

**Return the type of**: [<code>Contact</code>](/api/contact)


Get Contact by id
> Tips:
This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table)

**Kind**: static method of [<code>Contact</code>](/api/contact)  

| Param | Type |
| --- | --- |
| id | <code>string</code> | 

**Example**  
```js
const bot = new Wechaty()
await bot.start()
const contact = bot.Contact.load('contactId')
```
<a id="contactfind"></a>

## Contact.find(query)

**Return the type of**: <code>Promise.&lt;(Contact&#124;null)&gt;</code>


Try to find a contact by filter: {name: string | RegExp} / {alias: string | RegExp}

Find contact by name or alias, if the result more than one, return the first one.

**Kind**: static method of [<code>Contact</code>](/api/contact)  
**Returns**: <code>Promise.&lt;(Contact&#124;null)&gt;</code> - If can find the contact, return Contact, or return null  

| Param | Type |
| --- | --- |
| query | [<code>ContactQueryFilter</code>](/api/?id=contactqueryfilter) | 

**Example**  
```js
const bot = new Wechaty()
await bot.start()
const contactFindByName = await bot.Contact.find({ name:"ruirui"} )
const contactFindByAlias = await bot.Contact.find({ alias:"lijiarui"} )
```
<a id="contactfindall"></a>

## Contact.findAll([queryArg])

**Return the type of**: <code>Promise.&lt;Array.&lt;Contact&gt;&gt;</code>


Find contact by `name` or `alias`

If use Contact.findAll() get the contact list of the bot.

<h3>definition</h3>
- `name`   the name-string set by user-self, should be called name
- `alias`  the name-string set by bot for others, should be called alias

**Kind**: static method of [<code>Contact</code>](/api/contact)  

| Param | Type |
| --- | --- |
| [queryArg] | [<code>ContactQueryFilter</code>](/api/?id=contactqueryfilter) | 

**Example**  
```js
const bot = new Wechaty()
await bot.start()
const contactList = await bot.Contact.findAll()                    // get the contact list of the bot
const contactList = await bot.Contact.findAll({name: 'ruirui'})    // find allof the contacts whose name is 'ruirui'
const contactList = await bot.Contact.findAll({alias: 'lijiarui'}) // find all of the contacts whose alias is 'lijiarui'
```