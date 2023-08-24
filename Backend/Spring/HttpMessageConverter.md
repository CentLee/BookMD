# Http Message Converter

### HTTP API처럼 JSON 데이터를 HTTP 메시지 바디에서 직접 읽거나 쓰는 경우 HTTP 메시지 컨버터를 사용하면 편리하다.


#### 스프링 부트 기본 메시지 컨버터 (일부 생략)
#### 0 = ByteArrayHttpMessageConverter
#### 1 = StringHttpMessageConverter
#### 2 = MappingJackson2HttpMessageConverter

```java
public interface HttpMessageConverter<T> {
      boolean canRead(Class<?> clazz, @Nullable MediaType mediaType);
      boolean canWrite(Class<?> clazz, @Nullable MediaType mediaType);

      List<MediaType> getSupportedMediaTypes();
      T read(Class<? extends T> clazz, HttpInputMessage inputMessage)
              throws IOException, HttpMessageNotReadableException;
      void write(T t, @Nullable MediaType contentType, HttpOutputMessage
    outputMessage)
              throws IOException, HttpMessageNotWritableException;
}
```

#### HTTP 메시지 컨버터는 HTTP 요청, HTTP 응답 둘 다 사용된다.
#### canRead() , canWrite() : 메시지 컨버터가 해당 클래스, 미디어타입을 지원하는지 체크 
#### read() , write() : 메시지 컨버터를 통해서 메시지를 읽고 쓰는 기능


#### Http Message Converter 위치 
![스크린샷 2023-08-24 오후 6 44 35](https://github.com/CentLee/BookMD/assets/35019052/0a39fdc6-5cfd-451f-ae1b-b4e75828cf66)
