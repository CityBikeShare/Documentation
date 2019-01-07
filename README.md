# Documentation

## Predlagane mikrostoritve

1. Katalog razpoložljivih koles
    > omogoča prikazovanje koles, dodajanje novih koles za izposojo, posodabljanje že obstoječih in brisanje.

2. Izposoja in vrnitev kolesa
    > omogoča izposojo, vrnitev in prekinitev izposoje. 

3. Upravljanje z uporabniki
    > omogoča registracijo, prijavo, posodabljanje in izbris uporabniškega računa, ki se uporablja za objavo in izposojo koles.

4. Plačevanje
    > pregled nad izposojo, računanje dolga glede na število dni izposoje, plačevanje


## Koristni linki

- [GitHub](https://github.com/orgs/CityBikeShare/dashboard)

- [Travis](https://travis-ci.org/CityBikeShare)

- [DockerHub](https://hub.docker.com/u/citybikeshare)

- [Kubernetes](https://console.bluemix.net/containers-kubernetes/clusters/77a9d8f1d0d04857a4fa680904fca098/overview?region=ibm:yp:eu-de&resourceGroup=)

- [Logit.io](https://logit.io/a/5a3f88fc-ec2f-491e-a479-10351343c1ab)

- **Consul** http://159.122.177.235:30559/ui/dc1/services

---

### Osnovni docker ukazi

- **PostgreSQL** -> docker run -d --name cityBikeShare -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=cityBikeShare -p 5433:5432 postgres:latest
- **Consul** -> docker run -d -p 8500:8500 --name test consul agent -server -client 0.0.0.0 -ui -bootstrap-expect 1 -bind 127.0.0.1

---

### BikeCatalogService
    GET
        - localhost:8082/sources/bikes/                    ### Get all bikes
        - localhost:8082/sources/bikes/bike/{id}           ### Get bike by id
        - localhost:8082/sources/bikes/region/{region}     ### Get bikes in given region
        - localhost:8082/sources/bikes/user/{id}           ### Get bikes owned by user with given id

    PUT
        - localhost:8082/sources/bikes/insertNew           ### Inserts new bike in the catalog [@RequestBody Bikes]
        - localhost:8082/sources/bikes/update/{id}         ### Updated bike with given id to [@RequestBody Bikes]

    DELETE
        - localhost:8082/sources/bikes/delete/{id}         ### Deletes a bike from the catalog
        
### BikeRentService
    GET
        - localhost:8081/sources/bikerent/                      ### Get all bikes ever rented
        - localhost:8081/sources/bikerent/{id}                  ### Get bike rented by id

    POST
        - localhost:8081/sources/bikerent/rent                  ### Rent a bike [@QueryParam bikeId, @QueryParam userid]

    PUT
        - localhost:8081/sources/bikerent/return/{bikeid}       ### Return rented bike with given id
        
    DELETE
        - localhost:8081/sources/bikerent/{id}                  ### Delete bike record with bikeRent id 

### UserManagmentService
    GET
        - localhost:8080/sources/users                      ### Get all users
        - localhost:8080/sources/users/{id}                 ### Get user by id
        - localhost:8080/sources/users/region/{region}      ### Get users living in given region
        
    PUT
        - localhost:8080/sources/users/registerUser         ### User registration [@RequestBody Users]
        - localhost:8080/sources/users/update/{id}          ### Update a user by id with [@RequestBody Users]

    POST
        - localhost:8080/sources/users/loginUser            ### User login [@QueryParam uname, @QueryParam passwd]

    DELETE
        - localhost:8080/sources/users/delete/{id}          ### Delete user by id

### Poizvedbe po dnevnikih
    - marker.parents.name:METHOD            # Klici metod
    - contextMap.method:convertPrice        # Klic določene metode
    - contextMap.method:applicationName     # Klic določene storitve
    - level:error                           # Prikaz error sporočil