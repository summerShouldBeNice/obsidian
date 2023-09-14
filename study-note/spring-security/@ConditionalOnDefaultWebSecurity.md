-  是一个组合注解
```java
@Target({ElementType.TYPE, ElementType.METHOD})  
@Retention(RetentionPolicy.RUNTIME)  
@Documented  
@Conditional({DefaultWebSecurityCondition.class})  
public @interface ConditionalOnDefaultWebSecurity {  
}
```
- 主要是DefaultWebSecurityCondition.class条件装配
```java
class DefaultWebSecurityCondition extends AllNestedConditions {  
    DefaultWebSecurityCondition() {  
        super(ConfigurationPhase.REGISTER_BEAN);  
    }  
  
    @ConditionalOnMissingBean({WebSecurityConfigurerAdapter.class, SecurityFilterChain.class})  
    static class Beans {  
        Beans() {  
        }  
    }  
  
    @ConditionalOnClass({SecurityFilterChain.class, HttpSecurity.class})  
    static class Classes {  
        Classes() {  
        }  
    }  
}
```
- 会检查项目中有没有WebSecurityConfigurerAdapter这个bean或者有没有SecurityFilterChain和HttpSecurity这两个类如果有的话就不启用默认的配置
- 根据security文档，官方已经弃用WebSecurityConfigurerAdapter这个类