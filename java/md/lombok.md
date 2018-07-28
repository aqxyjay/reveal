# Project Lombok

---

## Lombok

一个极大简化Java代码开发的一个类库  

---

用了Lombok以后，不用花费过多精力来写：

`getter`        <!-- .element: class="fragment visible"-->  
`setter`        <!-- .element: class="fragment visible"-->  
`toString`      <!-- .element: class="fragment visible"-->  
`constructor`   <!-- .element: class="fragment visible"-->  
`equals`        <!-- .element: class="fragment visible"-->  
`builder`       <!-- .element: class="fragment visible"-->  
`log`           <!-- .element: class="fragment visible"-->  
`syncronized`   <!-- .element: class="fragment visible"-->  
`null check`   <!-- .element: class="fragment visible"-->  
`close stream`   <!-- .element: class="fragment visible"-->  

---

### `getter`/`setter`

`@Getter`

`@Setter`

--

#### 使用`@Getter`/`@Setter`前

```java
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public void setStatus(StatusEnum status) {
        this.status = status;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public StatusEnum getStatus() {
        return status;
    }

    public String getMessage() {
        return message;
    }

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.error);
        response.setMessage("No lombok error");
        System.out.println(response.getStatus());
        System.out.println(response.getMessage());
    }
}
```

--

#### 使用`@Getter`/`@Setter`后

```java
//也可以在类的头部进行标注
//@Getter
//@Setter
public class MessageResponse extends Response {

    @Getter
    @Setter
    private StatusEnum status;

    @Getter
    @Setter
    private String message;

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.success);
        response.setMessage("Lombok is good");
        System.out.println(response.getStatus());
        System.out.println(response.getMessage());
    }
}
```

---

### `toString`

`@ToString`

--

#### 使用`@ToString`前

```java
@Setter
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    @Override
    public String toString() {
        return "MessageResponse(" +
                "status=" + status +
                ", message=" + message +
                ')';
    }

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.error);
        response.setMessage("No lombok error");
        System.out.println(response.toString());
    }
}

Output: MessageResponse(status=error, message='No lombok error')
```

--

#### 使用`@ToString`后

```java
@Setter
@ToString
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.success);
        response.setMessage("Lombok is good");
        System.out.println(response.toString());
    }
}

Output: MessageResponse(status=success, message=Lombok is good)
```


---

### `constructor`

`@AllArgsConstructor`

`@RequiredArgsConstructor`

`@NoArgsConstructor`

--

#### 使用`@AllArgsConstructor`前

```java
@ToString
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public MessageResponse(StatusEnum status, String message) {
        this.status = status;
        this.message = message;
    }

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse(StatusEnum.success, "Lombok is good");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@AllArgsConstructor`后

```java
@ToString
@AllArgsConstructor
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse(StatusEnum.success, "Lombok is good");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@RequiredArgsConstructor`前

```java
@ToString
public class MessageResponse extends Response {

    private final StatusEnum status;

    private final String message;

    private MessageResponse(StatusEnum status, String message) {
        this.status = status;
        this.message = message;
    }

    public static MessageResponse instance(StatusEnum status, String message) {
        return new MessageResponse(status, message);
    }

    public static void main(String[] args) {
        MessageResponse response = MessageResponse.instance(StatusEnum.success, "Lombok is good");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@RequiredArgsConstructor`后

```java
@ToString
@RequiredArgsConstructor(staticName = "instance")
@AllArgsConstructor(access = AccessLevel.PRIVATE)
public class MessageResponse extends Response {

    private final StatusEnum status;

    private final String message;

    public static void main(String[] args) {
        MessageResponse response = MessageResponse.instance(StatusEnum.success, "Lombok is good");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@NoArgsConstructor`前

```java
@Setter
@ToString
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public MessageResponse() {
    }

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.error);
        response.setMessage("No lombok error");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@NoArgsConstructor`后

```java
@Setter
@ToString
@NoArgsConstructor
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.error);
        response.setMessage("No lombok error");
        System.out.println(response.toString());
    }
}
```

---

### `equals`

`@EqualsAndHashCode`

--

#### 使用`@EqualsAndHashCode`前

```java
@AllArgsConstructor
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        MessageResponse that = (MessageResponse) o;
        return status == that.status &&
                Objects.equals(message, that.message);
    }

    @Override
    public int hashCode() {
        return Objects.hash(status, message);
    }

    public static void main(String[] args) {
        MessageResponse response1 = new MessageResponse(StatusEnum.error, "No Lombok error");
        MessageResponse response2 = new MessageResponse(StatusEnum.error, "No Lombok error");
        System.out.println(response1.equals(response2));
    }
}

Output: true
```

--

#### 使用`@EqualsAndHashCode`后

```java
@AllArgsConstructor
@EqualsAndHashCode(callSuper = false)
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response1 = new MessageResponse(StatusEnum.sucess, "Lombok is good");
        MessageResponse response2 = new MessageResponse(StatusEnum.sucess, "Lombok is good");
        System.out.println(response1.equals(response2));
    }
}

Output: true
```

---

### `Data class`/`Immutable class`

`@Data`

`@Value`

--

#### 使用`@Data`前

```java
@Getter
@Setter
@ToString
@RequiredArgsConstructor(staticName = "of")
@AllArgsConstructor(access = AccessLevel.PROTECTED)
@EqualsAndHashCode(callSuper = false)
public class MessageResponse extends Response {

    private final StatusEnum status;

    private String message;
}
```

--

#### 使用`@Data`后

```java
@Data
public class MessageResponse extends Response {

    private final StatusEnum status;

    private String message;
}
```

--

#### 使用`@Value`前

```java
@Getter
@ToString
@EqualsAndHashCode
@AllArgsConstructor
public final class MessageResponse extends Response {

    private final StatusEnum status;

    private final String message;
}
```

--

#### 使用`@Value`后

```java
@Value
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;
}
```

---

### `builder`

`@Builder`

--

#### 使用`@Builder`前

```java
@Setter
@ToString
public class MessageResponse extends Response {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response = new MessageResponse();
        response.setStatus(StatusEnum.error);
        response.setMessage("No builder error");
        System.out.println(response.toString());
    }
}
```

--

#### 使用`@Builder`后

```java
@Builder
@ToString
public class MessageResponse {

    private StatusEnum status;

    private String message;

    public static void main(String[] args) {
        MessageResponse response = MessageResponse.builder().status(StatusEnum.success).message("Lombok builder is good").build();
        System.out.println(response.toString());
    }
}
```

---

### `log`

`@CommonsLog`

`@JBossLog`

`@Log`

`@Log4j`

`@Log4j2`

`@Slf4j`

`@XSlf4j`

--

#### 使用`@Slf4j`前

```java
public class LogExample {
    private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(LogExample.class);

    public static void main(String... args) {
        log.error("Something else is wrong here");
    }
}
```

--

#### 使用`@Slf4j`后

```java
@Slf4j
public class LogExample {

    public static void main(String... args) {
        log.error("Something else is wrong here");
    }
}
```

---

### `syncronized`

`@Synchronized`

--

#### 使用`@Synchronized`前

```java
public class SynchronizedExample {
    private static final Object $LOCK = new Object[0];
    private final Object $lock = new Object[0];
    private final Object readLock = new Object();

    public static void hello() {
        synchronized($LOCK) {
            System.out.println("world");
        }
    }

    public int answerToLife() {
        synchronized($lock) {
            return 42;
        }
    }

    public void foo() {
        synchronized(readLock) {
            System.out.println("bar");
        }
    }
}
```

--

#### 使用`@Synchronized`后

```java
public class SynchronizedExample {
    private final Object readLock = new Object();

    @Synchronized
    public static void hello() {
        System.out.println("world");
    }

    @Synchronized
    public int answerToLife() {
        return 42;
    }

    @Synchronized("readLock")
    public void foo() {
        System.out.println("bar");
    }
}
```

---

### `null check`

`@NonNull`

--

#### 使用`@NonNull`前

```java
public class NonNullExample extends Something {
    private String name;

    public NonNullExample(Person person) {
        super("Hello");
        if (person == null) {
            throw new NullPointerException("person");
        }
        this.name = person.getName();
    }
}
```

--

#### 使用`@NonNull`后

```java
public class NonNullExample extends Something {
    private String name;

    public NonNullExample(@NonNull Person person) {
        super("Hello");
        this.name = person.getName();
    }
}
```

---

### `close stream`

`@Cleanup`

--

#### 使用`@Cleanup`前

```java
public class CleanupExample {
    public static void main(String[] args) throws IOException {
        InputStream in = new FileInputStream(args[0]);
        try {
            OutputStream out = new FileOutputStream(args[1]);
            try {
                byte[] b = new byte[10000];
                while (true) {
                    int r = in.read(b);
                    if (r == -1) break;
                    out.write(b, 0, r);
                }
            } finally {
                if (out != null) {
                    out.close();
                }
            }
        } finally {
            if (in != null) {
                in.close();
            }
        }
    }
}
```

--

#### 使用`@Cleanup`后

```java
public class CleanupExample {
    public static void main(String[] args) throws IOException {
        @Cleanup InputStream in = new FileInputStream(args[0]);
        @Cleanup OutputStream out = new FileOutputStream(args[1]);
        byte[] b = new byte[10000];
        while (true) {
            int r = in.read(b);
            if (r == -1) break;
            out.write(b, 0, r);
        }
    }
}
```

---

### 参考

 - [Project Lombok](https://projectlombok.org)
 - [Lombok Features](https://projectlombok.org/features/all)
 - [Install Lombok on Eclipse](https://projectlombok.org/setup/eclipse)
 - [Install Lombok on IDEA](https://projectlombok.org/setup/intellij)

