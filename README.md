# zuul

Da bismo implementirali Zuul potrebno je:

1. dodati spring-cloud-starter-netflix-zuul dependecy u pom.xml fajl
2. dodati anotaciju @EnableZuulProxy u @SpringBootApplication klasu
3. dodati dodatne properties u application.properties fajl

Uz to ova aplikacija je i Eureka klijent pa je potrebno dodati i:

4. dodati spring-cloud-starter-netflix-eureka-client dependecy u pom.xml fajl
5. dodati anotaciju @EnableEurekaClient u @SpringBootApplication klasu
6. dodati dodatne properties u application.properties fajl
