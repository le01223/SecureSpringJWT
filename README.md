# SecureSpringJWT 🔐

Проект аутентификации и авторизации REST API с использованием:
- Spring Boot
- Spring Security
- JWT

## 📌 Технологии и версии

- Spring Boot `1.5.4.RELEASE`
- Spring Framework `4.3.9.RELEASE`
- Spring Security `4.2.3.RELEASE`
- Tomcat Embed `8.5.15`
- Joda DateTime `2.9.9`

## 🔐 Аутентификация

Доступно два способа входа:

### 1. Через JSON (/login)
```json
{
  "username": "user",
  "password": "test123"
}
```
### 2. Через форму (/loginForm)
Формат: x-www-form-urlencoded

Успешный ответ:

```text
eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJiaHIiLCJyb2xlIjoiQURNSU4iLCJleHAiOjE1MDcxMDg3MjJ9.-fkoAQ-u8zHQBE4OgayRtJOpSTaEEyaL1bbPRt-bRNUy_qarcA8zs_BQ4aIh8n4FcQ3eZbK8HzOHZ5JzX08Yhg
```
Ошибка:

```http
401 Unauthorized
```
### 🔒 Защищенные эндпоинты
Требуют валидного JWT-токена в заголовке:

```http
Authorization: Bearer ваш_токен
```
Доступные эндпоинты:
```
GET /api/hello/admin - для администраторов

GET /api/hello/user - для пользователей

POST /api/me - информация о текущем пользователе

POST /api/user - управление пользователями
```

🚀 Запуск проекта
Клонируйте репозиторий

Перейдите в папку проекта

Выполните:

Linux/macOS:

```bash
./mvnw clean spring-boot:run
```
Windows:

```cmd
mvnw.cmd clean spring-boot:run
```
Откройте в браузере:

```
http://localhost:8080/login
http://localhost:8080/loginForm
```

## 👥 Тестовые пользователи

| Роль         | Логин  | Пароль  |
|--------------|--------|---------|
| Пользователь | user   | test123 |
| Администратор| admin  | test123 |


Конфигурация пользователей в WebSecurityConfig.java:

```java
@Autowired
public void configureAuthentication(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication()
        .withUser("user").password("test123").roles("USER")
        .and()
        .withUser("admin").password("test123").roles("ADMIN");
}
```
