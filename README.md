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
- **Etcd** -> docker run -d -p 2379:2379 --name etcd --volume=/tmp/etcd-data:/etcd-data quay.io/coreos/etcd:latest /usr/local/bin/etcd --name my-etcd-1 --data-dir /etcd-data --listen-client-urls http://0.0.0.0:2379 --advertise-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-advertise-peer-urls http://0.0.0.0:2380 --initial-cluster my-etcd-1=http://0.0.0.0:2380 --initial-cluster-token my-etcd-token --initial-cluster-state new --auto-compaction-retention 1 -cors="*"
---

### BikeCatalogService
    GET
        - http://159.122.177.235:30000/sources/bikes/                    ### Get all bikes
        - http://159.122.177.235:30000/sources/bikes/bike/{id}           ### Get bike by id
        - http://159.122.177.235:30000/sources/bikes/region/{region}     ### Get bikes in given region
        - http://159.122.177.235:30000/sources/bikes/user/{id}           ### Get bikes owned by user with given id
        - http://159.122.177.235:30000/sources/bikes/convert/            ### Get bike price in other currency [@QueryParam bikeid, currency]
      
    PUT
        - http://159.122.177.235:30000/sources/bikes/insertNew           ### Inserts new bike in the catalog [@RequestBody Bikes]
        - http://159.122.177.235:30000/sources/bikes/update/{id}         ### Updated bike with given id to [@RequestBody Bikes]

    DELETE
        - http://159.122.177.235:30000/sources/bikes/delete/{id}         ### Deletes a bike from the catalog
        
### BikeRentService
    GET
        - http://159.122.177.235:30001/sources/bikerent/                      ### Get all bikes ever rented
        - http://159.122.177.235:30001/sources/bikerent/{id}                  ### Get bike rented by id

    POST
        - http://159.122.177.235:30001/sources/bikerent/rent                  ### Rent a bike [@QueryParam bikeId, @QueryParam userid]

    PUT
        - http://159.122.177.235:30001/sources/bikerent/return/{bikeid}       ### Return rented bike with given id
        
    DELETE
        - http://159.122.177.235:30001/sources/bikerent/{id}                  ### Delete bike record with bikeRent id 

### UserManagmentService
    GET
        - http://159.122.177.235:30002/sources/users                      ### Get all users
        - http://159.122.177.235:30002/sources/users/{id}                 ### Get user by id
        - http://159.122.177.235:30002/sources/users/region/{region}      ### Get users living in given region
        
    PUT
        - http://159.122.177.235:30002/sources/users/registerUser         ### User registration [@RequestBody Users]
        - http://159.122.177.235:30002/sources/users/update/{id}          ### Update a user by id with [@RequestBody Users]

    POST
        - http://159.122.177.235:30002/sources/users/loginUser            ### User login [@QueryParam uname, @QueryParam passwd]

    DELETE
        - http://159.122.177.235:30002/sources/users/delete/{id}          ### Delete user by id

### Poizvedbe po dnevnikih
    - marker.parents.name:METHOD                        # Klici metod
    - contextMap.method:getAllBikes                     # Klic določene metode
    - contextMap.applicationName:bikecatalogservice     # Klic določene storitve
    - level:error                                       # Prikaz error sporočil