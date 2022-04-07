# EnterFullGroupWhatsapp
Paste this Code at Whatsapp-Web's console and put the invite code as the start function's arguement:
```js
const moduleRaid = function () {
  moduleRaid.mID  = Math.random().toString(36).substring(7);
  moduleRaid.mObj = {};
 
  fillModuleArray = function() {
    (window.webpackChunkbuild || window.webpackChunkwhatsapp_web_client).push([
      [moduleRaid.mID], {}, function(e) {
        Object.keys(e.m).forEach(function(mod) {
          moduleRaid.mObj[mod] = e(mod);
        })
      }
    ]);
  }
 
  fillModuleArray();
 
  get = function get (id) {
    return moduleRaid.mObj[id]
  }
 
  findModule = function findModule (query) {
    results = [];
    modules = Object.keys(moduleRaid.mObj);
 
    modules.forEach(function(mKey) {
      mod = moduleRaid.mObj[mKey];
 
      if (typeof mod !== 'undefined') {
        if (typeof query === 'string') {
          if (typeof mod.default === 'object') {
            for (key in mod.default) {
              if (key == query) results.push(mod);
            }
          }
 
          for (key in mod) {
            if (key == query) results.push(mod);
          }
        } else if (typeof query === 'function') { 
          if (query(mod)) {
            results.push(mod);
          }
        } else {
          throw new TypeError('findModule can only find via string and function, ' + (typeof query) + ' was passed');
        }
 
      }
    })
 
    return results;
  }
 
  return {
    modules: moduleRaid.mObj,
    constructors: moduleRaid.cArr,
    findModule: findModule,
    get: get
  }
}
 
if (typeof module === 'object' && module.exports) {
  module.exports = moduleRaid;
} else {
  window.mR = moduleRaid();
}
const m = new moduleRaid()
 
const sleep = (ms) => {
  return new Promise((resolve) => setTimeout(resolve, ms));
};
const getInfo = m.findModule("sendQueryGroupInvite")[0].sendQueryGroupInvite;
const joinGroup = m.findModule("sendJoinGroupViaInvite")[0].sendJoinGroupViaInvite;
let start = async (code)=>{
    while((await getInfo(code)).size===257){
        await sleep(5000);
    }
    await joinGroup(code);
}
start("Invite code HERE")
```
