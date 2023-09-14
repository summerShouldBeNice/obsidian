1. 用户在前端发送post请求
2. SpringBootWebSecurityConfiguration配置类的[[@ConditionalOnDefaultWebSecurity]]条件满足所以会自动装配这个类

```java
@Configuration(  
    proxyBeanMethods = false  
)  
@ConditionalOnDefaultWebSecurity  
static class SecurityFilterChainConfiguration {  
    SecurityFilterChainConfiguration() {  
    }  
  
    @Bean  
    @Order(2147483642)  
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {  
        ((ExpressionUrlAuthorizationConfigurer.AuthorizedUrl)http.authorizeRequests().anyRequest()).authenticated();  
        http.formLogin();  
        http.httpBasic();  
        return (SecurityFilterChain)http.build();  
    }  
}
```
3. 如果没有自定义配置就使用默认的认证规则由于前端发送的是post请求所以认证的方法主要是HttpSecurity的formLogin方法
```java
public FormLoginConfigurer<HttpSecurity> formLogin() throws Exception {  
    return (FormLoginConfigurer)this.getOrApply(new FormLoginConfigurer());  
}
```
4. 这个方法创建了一个FormLoginConfigurer对象
```java
public FormLoginConfigurer() {  
    super(new UsernamePasswordAuthenticationFilter(), (String)null);  
    this.usernameParameter("username");  
    this.passwordParameter("password");  
}
```
5. FormLoginConfigurer对象创建时创建了一个UsernamePasswordAuthenticationFilter的过滤器
```java
public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException {  
    if (this.postOnly && !request.getMethod().equals("POST")) {  
        throw new AuthenticationServiceException("Authentication method not supported: " + request.getMethod());  
    } else {  
        String username = this.obtainUsername(request);  
        username = username != null ? username.trim() : "";  
        String password = this.obtainPassword(request);  
        password = password != null ? password : "";  
        UsernamePasswordAuthenticationToken authRequest = UsernamePasswordAuthenticationToken.unauthenticated(username, password);  
        this.setDetails(request, authRequest);  
        return this.getAuthenticationManager().authenticate(authRequest);  
    }  
}
```
6. 由于UsernamePasswordAuthenticationFilter不是原生的filter所以没有原生的doFilter方法而是由attemptAuthentication方法来进行认证，在attemptAuthentication方法内首先获取了请求的方法是不是post如果不是直接返回并抛出异常，如果是则调用obtain方法从HttpServletRequest中获取用户名和密码
```java
@Nullable  
protected String obtainPassword(HttpServletRequest request) {  
    return request.getParameter(this.passwordParameter);  
}  
  
@Nullable  
protected String obtainUsername(HttpServletRequest request) {  
    return request.getParameter(this.usernameParameter);  
}
```
7. 然后UsernamePasswordAuthenticationToken调用unauthenticated方法使用用户名和密码入参实例化
```java
public static UsernamePasswordAuthenticationToken unauthenticated(Object principal, Object credentials) {  
    return new UsernamePasswordAuthenticationToken(principal, credentials);  
}


public UsernamePasswordAuthenticationToken(Object principal, Object credentials) {  
    super((Collection)null);  
    this.principal = principal;  
    this.credentials = credentials;  
    this.setAuthenticated(false);  
}
```
8. 然后调用setDetails方法
```java
protected void setDetails(HttpServletRequest request, UsernamePasswordAuthenticationToken authRequest) {  
    authRequest.setDetails(this.authenticationDetailsSource.buildDetails(request));  
}
```
9. 方法是由UsernamePasswordAuthenticationToken进行调用的UsernamePasswordAuthenticationToken继承了AbstractAuthenticationToken所以调用的是AbstractAuthenticationToken的setDetails方法,就是将http请求中数据放入到private Object details里
```java
public void setDetails(Object details) {  
    this.details = details;  
}
```
10. 然后调用this.getAuthenticationManager().authenticate(authRequest)进行校验