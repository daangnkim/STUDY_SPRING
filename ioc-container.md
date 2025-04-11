IoC는 객체의 생성과 관리를 개발자가 아닌 framework에게 맡기는 것을 의미한다. 전통적으로 객체의 생성과 관리를 개발자가 담당했으나, IoC는 이 책임을 프레임워크에게 전가한다. 그리고 IoC Container는 스프링 부트의 코어 컴포넌트로, (1) bean의 라이프 사이클을 다루며, (2) bean의 생성과 인스턴스화하고, (3) 필요한 곳에 주입하는 역할을한다.

Spring Boot는 IoC를 DI를 이용하여 구현하며, 런타임에 의존성을 주입한다.

## IoC Container의 종류

1. BeanFactor

- 의존성 주입을 제공하는 가장 기본적인 IoC Container다.

2. ApplicationContext

- 더 진보된 Container로 이벤트 전파, bean 생성을 위한 선언적 메커니즘등을 제공한다.

## DI의 종류

1. Constructor Injection

- constructor를 통해서 의존성이 주입된다.

2. Setter Injection

- setter 메서드를 통해서 의존성이 주입된다.

3. Field Injection

- field에 바로 의존성이 주입된다.

## 예제

알람 서비스는 email과 SMS를 이용하고, 이러한 서비스는 환경 설정과 의존성이 필요하다.

1. Notification Service를 위한 인터페이스 만들기

```java
public interface NotificationService {
    void sendNotification(String message);
}
```

2. Email과 SMS 각각을 위한 Notification Service 구현

```java
import org.springframework.stereotype.Service;

@Service
public class EmailNotificationService implements NotificationService {

    @Override
    public void sendNotification(String message) {
        System.out.println("Sending email notification: " + message);
    }
}
```

```java
import org.springframework.stereotype.Service;

@Service
public class SmsNotificationService implements NotificationService {

    @Override
    public void sendNotification(String message) {
        System.out.println("Sending SMS notification: " + message);
    }
}
```

3. Notification Controller 정의하고 constructor based로 의존성 주입하기

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class NotificationController {

    private final EmailNotificationService emailNotificationService;
    private final SmsNotificationService smsNotificationService;

    @Autowired
    public NotificationController(EmailNotificationService emailNotificationService,
                                  SmsNotificationService smsNotificationService) {
        this.emailNotificationService = emailNotificationService;
        this.smsNotificationService = smsNotificationService;
    }

    @GetMapping("/sendEmail")
    public String sendEmail(@RequestParam String message) {
        emailNotificationService.sendNotification(message);
        return "Email notification sent!";
    }

    @GetMapping("/sendSms")
    public String sendSms(@RequestParam String message) {
        smsNotificationService.sendNotification(message);
        return "SMS notification sent!";
    }
}
```

4. Application Setup

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class NotificationServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(NotificationServiceApplication.class, args);
    }
}
```

애플리케이션이 시작되면 Spring Boot는 자동으로 Stereotype Annotation을 스캔한뒤 bean으로 등록한다.

## References

[Understanding IoC Container in Spring Boot with a Real-Time Project Example | by A cup of JAVA coffee with NeeSri | Medium](https://neesri.medium.com/understanding-ioc-container-in-spring-boot-with-a-real-time-project-example-6e28519ab444)
