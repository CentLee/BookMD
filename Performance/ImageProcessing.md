# Image Processing

- 이미지 처리에 관한 최적화에 대한 방법?

- 보편적으로 알고 있는 최적화는 원하는 뷰 프레임에 맞춰서 이미지를 작게 축소하는 resize가 있다.
- 이에 대해 사용할 수 있는 UIGraphicsBeginImageContext 와 UIGraphicsImageRenderer 두 가지가 존재한다.
- 이미지를 많이 사용하다보면 instruments profiling 의 memory leak을 돌려보면 유난히 UIImage와 관련된 곳에서 메모리와 cpu점유율이 많이 증가한다.
- 당연히 그래픽과 관련된 내용이므로 증가하는 것이 맞으나, 이미지의 양에 따라 최적화할 필요가 있다. 
- UIImage = Data 타입인데, 이 데이터를 디코딩해서 실제 이미지로 만드는 과정에서 많은 비용이 든다.

## UIGraphicsBeginImageContext 
- four bytes per pixel
- Creates a bitmap-based graphics context and makes it the current context.
- 현 컨텍스트를 비트맵을 베이스로 하는 그래픽 컨텍스트로 만드는 함수
- SRGB 형식과 스택을 이용한다. 
- 관련된 함수로는 UIGraphicsEndImageContext() 와 UIGraphicsGetImageFromCurrentImageContext() -> UIImage? 가 있다.
- 동작은 현 함수로 컨텍스트를 생성하고 그에 대한 처리를 하고 UIGraphicsGetImageFromCurrentImageContext로 이미지 가져오고 끝내면서 스택에 있던 컨텍스트를 제거하는 것까지의 과정을 거친다.

## UIGraphicsImageRenderer
- eight bytes per pixel
- UIGraphicsRenderer의 하위 클래스이며, 상위 추상 클래스이기 때문에 직접적 사용대신 Image or PDF Renderer을 사용한다.
- 위와 다른 것은 코어 그래픽 이미지를 지원하기 위해 사용하는 클래스이다.
- 색상 깊이 및 이미지 스케일과 같은 구성을 처리하거나 Core Graphics 컨텍스트를 관리하지 않고도 그리기 작업을 수행할 수 있게 해준다.

```swift
let renderer = UIGraphicsImageRenderer(size: CGSize(width: 200, height: 200))

let image = renderer.image { (context) in
  UIColor.darkGray.setStroke()
  context.stroke(renderer.format.bounds)
  
  // 1) default Creating Image
  UIColor(colorLiteralRed: 158/255, green: 215/255, blue: 245/255, alpha: 1).setFill()
  context.fill(CGRect(x: 1, y: 1, width: 140, height: 140))
  
  // 2) Using Blending
  UIColor(colorLiteralRed: 145/255, green: 211/255, blue: 205/255, alpha: 1).setFill()
  context.fill(CGRect(x: 60, y: 60, width: 140, height: 140), blendMode: .multiply) 
  
  // 3) Core Graphics Context 
  UIColor(colorLiteralRed: 203/255, green: 222/255, blue: 116/255, alpha: 0.6).setFill()
  context.cgContext.fillEllipse(in: CGRect(x: 60, y: 60, width: 140, height: 140)) 
}
```

## Down Sampling
- 위 방법에서 더 Low-Level 차원의 방법이 존재한다.
- 이미지 자체의 픽셀을 조절해서 비용을 줄이는 방법이다.

```swift
    let imageSourceOption = [kCGImageSourceShouldCache: false] as CFDictionary
    // 이미지 소스 옵션을 통해서 ImageData와 함께 이미지 소스를 만든다.
    
    let downSampleOptions = [
        kCGImageSourceCreateThumbnailFromImageAlways: true,
        kCGImageSourceShouldCacheImmediately: true,
        kCGImageSourceCreateThumbnailWithTransform: true,
        kCGImageSourceThumbnailMaxPixelSize: maxPixel
    ] as CFDictionary
    //위에서 만들어진 이미지 소스에 다운 샘플링 옵션을 더해서 새로운 이미지(픽셀이 조절된)를 만든다.
```


