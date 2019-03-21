|名称|类型|概述|
|------|------|------|
|工厂模式|创建型|生产实例的工厂。
|单例模式|创建型|一个进程只有一个实例。
|原型模式|创建型|克隆一个新实例。
|代理模式|结构型|假手于人。
|委派模式|行为型|甩手掌柜。
|策略模式|行为型|照方抓药。
|模板模式|行为型|实现当年吹过的牛逼。
|适配器模式|结构型|把不合适的整合适。
|装饰者模式|结构型|如虎添翼。
|观察者模式|行为型|行监坐守。

### SpringAOP示例：
```JAVA
@Component
@Aspect
public class LogAop {
    private Logger logger = LoggerFactory.getLogger(getClass());

    @Pointcut("execution(com.xxx.xxx.*(..))")
    public void pointcut() {
    }

    @Before("pointcut()")
    public void methodBefore(JoinPoint joinPoint) {
        logger.info("--- {} 方法前, 参数: {}---", joinPoint.getSignature().toShortString(), joinPoint.getArgs());
    }

    @AfterReturning(pointcut = "pointcut()", returning = "retVal")
    public void methodAfter(JoinPoint joinPoint, Object retVal) {
        logger.info("--- {} 方法后, 参数: {}---", joinPoint.getSignature().toShortString(), joinPoint.getArgs());
    }

    @AfterThrowing(pointcut = "pointcut()", throwing = "exception")
    public void methodException(JoinPoint joinPoint, Exception exception) {
        logger.info("--- {} 方法错误。信息: {}---", joinPoint.getSignature().toShortString(), exception.getMessage());
    }
}
```

### Spring IOC、DI示例：
```JAVA
//由容器创建Bean
@Service
public class UserServiceImpl implements UserService {
  //省略
}

//容器注入Bean
@Autowired
UserService userService;
//---------------------另一种获取方式--------------------------------
BeanFactory factory = WebApplicationContextUtils.getRequiredWebApplicationContext(request.getServletContext());
userService = factory.getBean(UserService.class);
```
