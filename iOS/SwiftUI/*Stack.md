
# *Stack 

* Likely UIStackView

- ZStack HStack VStack 등에 속성을 적용하면 Stack 안에 포함한 뷰 모두에게 적용할 수 있다.
- 각 뷰에 적용하면 각 뷰만 적용

```swift
var body: some View {
        ZStack(content: {
            RoundedRectangle(cornerRadius: 10)
                .stroke()
                .foregroundColor(.blue) << 이 코드가 우선 
                
            Text("TestView")
                .padding()

        }).foregroundColor(.red) 
}
```
- 이때 각 뷰와 스택뷰 자체에 적용됐다면 각 뷰에 적용된 속성의 우선순위가 더 높게 적용돼 각 뷰에 적용된 속성이 화면에 반영된다.
