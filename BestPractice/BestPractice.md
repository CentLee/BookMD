# Best Practice in iOS 


## Protocol Inherit 
- 프로토콜 상속 시에 가독성있게 Extension을 활용해서 분리하는 방법이 더 좋다.

Not Preferred 
``` swift
class example: UIViewController, UITableViewDataSource 
```

Preferred
``` swift 
class MyViewcontroller: UIViewController {
  ...
}

// MARK: - UITableViewDataSource

extension MyViewcontroller: UITableViewDataSource {
  // Table view data source methods
}

// MARK: - UIScrollViewDelegate

extension MyViewcontroller: UIScrollViewDelegate {
  // Scroll view delegate methods
}
```
