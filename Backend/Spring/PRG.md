# POST Redirect Get

#### Html Form 데이터를 서버로 전송해서 특정 작업을 진행할 때 폼 내부에서 Post action을 통해서 작업을 하게 될 때, 새로고침을 하면 Post가 중복으로 동작하게 된다. 
#### 이를 방지하기 위해서 Redirect를 사용하게 되는데

#### redirect: < 를 사용해서 동적 뷰의 경로를 제공하여 문제점을 해결한다

#### 다만 redirect 사용시 아래의 방식으로 사용하면 URL 인코딩이 안되기때문에 위험하다 고로, RedirectAttribute를 사용한다.
```java
    return "redirect:/basic/items" + item.getId(); 

    RedirectAttributes redirectAttributes 를 사용하여 
    redirectAttributes.addAttribute("itemId", savedItem.getId()); 
    return "redirect:/basic/items/{itemId}"; 이런 방식으로 사용한다. 
```
