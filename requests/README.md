### GET Requests

- Get all available bikes in the catalog -> http://localhost:8080/sources/bikes
- Get bike in the catalog, identified by id -> http://localhost:8080/sources/bikes/bike/{id}
- Get bikes in the catalog, identified by region of renting -> http://localhost:8080/sources/bikes/{region}

- Get all bikes currently rented -> http://localhost:8080/sources/bikerent
- Get bike rent, identified by id -> http://localhost:8080/sources/bikerent/{id}

### POST Requests

- Login to an account -> http://localhost:8080/sources/loginUser?uname=username&passwd=password

### PUT Requests

- Insert new bike in the catalog for rent -> http://localhost:8080/sources/bikes/insertNew
    
        Body: {
            "user_id": 1,
            "type": "",
            "size": "",
            "description": "",
            "price": 1,
            "available": true
        }


- Rent a bike -> http://localhost:8080/sources/bikerent

        Body: {
            "bike_id": 1,
            "user_id": 1,
            "debtSettled": false
        }

- Register a new user -> http://localhost:8080/sources/registerUser

        Body: {
            "name": "",
            "surname": "",
            "username": "",
            "password": "",
            "email": "",
            "region": ""
        }

### DELETE Requests

- Delete bike from the catalog -> http://localhost:8080/sources/bikes/bike/{id}

- Delete bike rent -> http://localhost:8080/sources/bikerent/{id}
