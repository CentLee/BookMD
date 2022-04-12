# How to Organize APIs And Endpoints 
  - API와 Endpoint들을 잘 관리하는 방법에 대한 글
  - Protocol 과 Enum을 활용하여 관리한다. 
  - 여러 api가 존재하고 그에따른 엔드포인트들도 다양하고 조금 더 코드 라인도 줄이고 가볍게 관리할 수 있게 제고하는 방법


# Simple Example

  ```swift
  protocol API {
    static var baseUrl: URL { get }
  } 
  
  
  enum APIs {
  
    enum Auth: String, API {
      static let baseUrl: URL = URL(string: "api 주소")!
      
      case logout = "logout api"
      case updateInfo = "update api"
    }
  }
  
  extension RawRepresentable where RawValue == String Self: API {
     var url: URL { Self.baseUrl.appendingPathComponent(RawValue) }
  }
  
  let url = APIs.Auth.logout.url
  
  ```
  
# Use enum associated values to pass in path parameters
  ```swift
  public protocol RawRepresentable {
    associatedType RawValue
    init?(rawValue: Self.RawValue) { nil }
    var rawValue: Self.RawValue { get }
  }
  
  extension APIs {
    enum Message: RawRePresentable, API {
      init?(rawValue: Self.RawValue) { nil }
      static let baseUrl: URL = URL(string: "api 주소")!
      
      case fetch
      case fetchEachTopic(topicDID: String)
      
      var rawValue: Self.RawValue {
        switch self {
          case .fetch:
            return "주소"
          case fetchEachTopic(let topicDID):
            return "주소\(topicDID)"
        }
      }
    }
  }
  
  let url = APIs.Message.fetchEachTopic(topicDID: "토픽아이디").url
  ```
