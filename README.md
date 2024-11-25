##
```sh
docker network create rpa
docker run --network rpa --name rpa-mysql -p 3306:3306 -d rpa-mysql:latest
docker run --network rpa --name rpa-frontend -p 3000:80 -d rpa-frontend:latest
docker run --network rpa --name rpa-backend -e "SPRING_DATASOURCE_URL=jdbc:mysql://rpa-mysql:3306/product" -p 8080:8080 -d rpa-backend:latest
```

### React Product App using Spring Boot as the backend
![alt text](react-product-app.png)