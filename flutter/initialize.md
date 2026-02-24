# Initialize SDK

### init()
Initialization PubStar SDK. Initialization must be called once before loading or showing ads.

### Example

```dart
import 'package:pubstar_io/pubstar_io.dart';

try {
    const result = await PubstarIo.init();
    // call when init done (ready to call load and show ad)
} on PubstarIoException catch (e) {
    // callback when init error
}
```
