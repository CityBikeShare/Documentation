## Documentation

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
