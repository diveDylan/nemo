
[English](Readme.en.md)

<h1 style="text-align: center">nemoð </h1>
<div style="text-align: center">
<img src="https://img.shields.io/npm/v/@dylan92/nemo?color=%23&style=plastic" />
<img src="https://img.shields.io/npm/l/@dylan92/nemo" />
<img src="https://img.shields.io/travis/com/diveDylan/nemo?style=plastic"/>
<img src="https://img.shields.io/codecov/c/github/diveDylan/nemo?style=plastic"/>
<img src="https://img.shields.io/npm/dm/@dylan92/nemo?style=plastic">
<img src="https://img.shields.io/badge/pkg--manage-pnpm-orange">
</div>
<p style="text-align: center"> 
ä¸ä¸ªèªå¨åçæ <code>swagger typescript</code> æä»¶çðªå·¥å·ï¼åºäº <code>swagger V2</code>
</p>


## å®è£

```node
  npm install @dylan92/nemo
  // or
  yarn add @dylan92/nemo
```

## æå»º

```zsh
# https://github.com/grosser/wwtd
gem install wwtd
# then
wwtd

```




## ç¨æ³

### åæ°:
  
  1. `url`: `swagger` é¡¹ç®ç `api json` å°å
  2. `output`: `typescript` æä»¶çè¾åºç®å½
  3. `requestPath`: ç¬¬ä¸æ¹è¯·æ±åºï¼å¦æéè¦èªå®ä¹è¯·æ±
  4. `exportsRequest`: æ¯å¦éè¦åæ¬¡è¾åºè¯·æ±ç®å½
  5. `paths`: è·¯å¾ï¼ç¨äºè¾åºå¶å®è·¯å¾çæä»¶

```typescript

interface SwaggerConfig {
  /**
   * @description swagger api url
   */
  url: string
  /**
   * @description single-api or apis
   */
  paths?: Array<string | Regexp>
  /**
   * @description output floder
   */
  output?: string
  /**
   * @description where request module import from
   */
  requestPath?: string
  /**
   * @description request templates only create and remove when it is true
   * when you only need exportsRequest once, mostly code likes:
   * * `exportsRequest: !isRequestFloderExsit`
   */
  exportsRequest?: boolean
}
```
å¨ä½ çé¡¹ç®æ°å»ºä¸ä¸ª `swagger.js` æä»¶ï¼å¤å¶ä¸ä¸ä»£ç ï¼ç¶å `node swagger.js`ï¼èæ¬ä¼èªå¨çæ `models`ã`services` ç®å½åä¸ä¸ªå¯¼åºæä»¶
```node
// swagger.js
const main = require('@dylan92/nemo')

// with esm
import main from '@dylan92/nemo'

main({
  url: 'https://petstore.swagger.io/v2/swagger.json',
  output: './src/core/test'
})

```
åªéè¦ä¸¤åéå³å¯æ¥å¥ç¬¬ä¸æ¹åºï¼ä½ éè¦å¤§æ¦äºè§£å¥åç `interface` ï¼ç¶åä¹¦åè½¬æ¢ä¸ä¸ªç®æè½¬æ¢å½æ°å³å¯å¼ç®±å³ç¨

```typescript
type RequestInitWithoutBodyInit = Omit<RequestInit, 'body'>

interface Options extends RequestInitWithoutBodyInit, Record<string, any> {
  body?: Record<string, any>
  formData?: Record<string, any>
  query?: Record<string, any>
}
// default request
request<ResponseType>(url: string, options: Options)


// your request file
import fetch from `${library}`
import { getRequestBody, Options  } from `${output}/utils`
// ä½ çè½¬æ¢å½æ°
export default async function <T>(url, options) {
  const body: BodyInit | undefined = getRequestBody(options)
  const data = await request<T>(url, Object.assign(options, {body}))
  return data
}
```


