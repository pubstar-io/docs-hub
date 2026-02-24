# Get UIViewController in SwiftUI

Get the current UIViewController in SwiftUI

### 1 If you want to get the current UIViewController in SwiftUI
You can use the following code:

```swift
var viewController: UIViewController = PubStarUtils.getHostingViewController()
```

### 2 If you want to use callback to get the UIViewController
You can use the following code:

```swift
struct UIViewGetter: UIViewRepresentable {
    let onReceive: (UIView) -> Void

    func makeUIView(context: Context) -> UIView {
        let view = UIView()
        DispatchQueue.main.async {
            self.onReceive(view)
        }
        return view
    }

    func updateUIView(_ uiView: UIView, context: Context) {}
}

struct ContentView: View {
    @State private var viewController: UIViewController?

    var body: some View {
        VStack {
            Color.gray.opacity(0.1)
                .frame(height: 300)
                .frame(maxWidth: .infinity)
                .background(
                    UIViewGetter { view in
                        self.customView = view
                    }
                )
        }
        .getViewControllerPubStar { controller in
            viewController = controller
        }
    }
}
```