# EnterFullGroupWhatsapp
Paste this Code at Whatsapp-Web's console and put the invite code as the start function's arguement:
```js
const getInfo = require('WAWebGroupQueryBridge').sendQueryGroupInvite;
const joinGroup = require("WAWebGroupInviteJob").joinGroupViaInvite;
let start = async (link) => {
  const code = new URL(link).pathname.slice(1);
  let info = await getInfo(code)
  while (info.size > 1024) {
    await new Promise((resolve) => setTimeout(resolve, 10000));
    console.log(`Current participants: ${info.size}`);
    info = await getInfo(code);
  }
  await joinGroup(code, false);
  console.log('Joined!');
}
await start("Invite link HERE");
```
press Enter and let it run.
You will join the group when someone will leave.
