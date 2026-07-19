---
title: Request Lifecycle
aliases:
  - Request Lifecycle
domain: Spring
module: Spring MVC
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - spring
---

# Request Lifecycle

Flow:
1. Client Request
2. DispatcherServlet
3. Handler Mapping
4. Controller
5. Service
6. Repository
7. Database
8. Response returned to client

This is a common interview topic.

Browser  
   ↓  
TCP Socket  
   ↓  
Tomcat Connector  
   ↓  
Thread Pool  
   ↓  
DispatcherServlet  
   ↓  
HandlerMapping  
   ↓  
HandlerAdapter  
   ↓  
Controller  
   ↓  
Service  
   ↓  
Repository  
   ↓  
Database  
   ↓  
Repository  
   ↓  
Service  
   ↓  
Controller  
   ↓  
HttpMessageConverter  
   ↓  
HttpServletResponse  
   ↓  
Tomcat  
   ↓  
Socket  
   ↓  
Browser
