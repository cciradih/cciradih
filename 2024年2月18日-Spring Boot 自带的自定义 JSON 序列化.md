# Spring Boot 自带的自定义 JSON 序列化
在实际业务中可能会遇到需要数据脱敏，而存储在数据库里的信息是明文的场景。这种情况下我们可以使用 Spring Boot 自带的自定义 JSON 序列化来实现。
## 自定义 JSON 序列化
```java
public class PhoneNumberSerializer extends JsonSerializer<String> {
    @Override
    public void serialize(String value, JsonGenerator gen, SerializerProvider serializers) throws IOException {
        if (StringUtils.hasText(value) && value.length() == 11) {
            String mask = "****";
            String prefix = value.substring(0, 3);
            String suffix = value.substring(value.length() - 4);
            String desensitization = prefix + mask + suffix;
            gen.writeString(desensitization);
        } else {
            gen.writeString(value);
        }
    }
}
```
继承的 JsonSerializer 需提供一个被序列化的类型，在这里是 String 类型的手机号。同时还需要实现一个抽象方法 serialize()。具体的反序列行为根据实际业务来决定，在这里是把手机号的中间四位字符串替换为****。
## 示例用户视图类
```java
@Data
public class UserView {
    @JsonSerialize(using = PhoneNumberSerializer.class)
    private String phoneNumber;
}
```
通过 JsonSerialize 注解中的 using 来配置使用自定义序列化。
## 示例控制器类
```java
@RestController
@RequestMapping("/demo")
public class DemoController {
    @GetMapping
    public UserView get() {
        UserView userView = new UserView();
        userView.setPhoneNumber("11122223333");
        return userView;
    }
}
```
在这里模拟了从数据库中读取的用户数据，请求 /demo 的响应如下：
```json
{
    "phoneNumber": "111****3333"
}
```
需要注意的是序列化发生在控制器方法返回后。
