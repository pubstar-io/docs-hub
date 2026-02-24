# Initialize SDK

### initialization()
Initialization PubStar SDK. Initialization must be called once before loading or showing ads.

### Example

```js
import Pubstar, { PubstarAdView } from 'rtn-pubstar';

try {
    const result = await Pubstar.initialization();
    // call when init done (ready to call load and show ad)
} catch(error) {
    // callback when init error
}
```
