# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [X] Commit: `Create Subscriber model struct.`
    -   [X] Commit: `Create Notification model struct.`
    -   [X] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [X] Commit: `Implement add function in Subscriber repository.`
    -   [X] Commit: `Implement list_all function in Subscriber repository.`
    -   [X] Commit: `Implement delete function in Subscriber repository.`
    -   [X] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [X] Commit: `Create Notification service struct skeleton.`
    -   [X] Commit: `Implement subscribe function in Notification service.`
    -   [X] Commit: `Implement subscribe function in Notification controller.`
    -   [X] Commit: `Implement unsubscribe function in Notification service.`
    -   [X] Commit: `Implement unsubscribe function in Notification controller.`
    -   [X] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [X] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [X] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [X] Commit: `Implement publish function in Program service and Program controller.`
    -   [X] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [X] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. As for now, I see that there is no need to use an interface or 'trait in this case because we are using rust. This is because I didn't see any other struct that behaves like subscriber did, so I don't think BambangShop needs an interface or 'trait' for the Subscriber, we can use an interface or trait if we wanted to use different implementations for subscribers, for example if we wanted to change the notifactions that are sent we can just simply make this a trait for different use cases of the interface/trait subscribers.

2. In my understanding, DashMap acts like Map in python and HashMap in Java, being so, it is more convinient to use DashMap to store items that have some sort of a primary key, we can use a vec/list, but the program needs to iterate the whole lists to check for duplicates but with DashMap, we can check if an item that has a specific key already exists or not.

3. After doing some googling about singleton especially in rust, I found that many people thinks that singletons aren't generally a good design practice because it is hard to do unit test properly with it. So, eventhough singleton can be used to manage a shared state like the list of subscribers, using DashMap is way better in rust.

#### Reflection Publisher-2

1. The need to separate the Service and Repository is to comply to the design princples within the MVC, including the Single Responsibility Principle (SRP), this means that we have Separation of Concerns and that each module only have one responsibility, therefore when it needed to be changed, it only changes for a specific reason and by doing so, increases the app's maintanability and flexibility.

2. Program will most likely be the core domain and logic of the app and without the separation with service and controller, program will not only handle data storage but also logics related to the program. For the notification and subscriber, the logics in those two models will most likely intertwined with the ones in the Program, thus making code duplications, furthermore, with no SoC, the code will be much harder to modify therefore making it harder to maintain.

3. Postman can help API testing like shown in this tutorial, postman also makes automation possible, and can generate API documentation from the request we made. 
#### Reflection Publisher-3

1. In this tutorial we are using the push model, this is because NotificationService pushes data to the subscriber everytime a subscriber uses the update method.

2. By using the pull model, the observer(subscriber) is not constantly polled for new information like the ones happening in the push model, in the pull model, since the observer pulls data from the publisher, observers can choose when do they want to get new information, the disadvantage of using the pull model is that it exposes the Subject to the Observer which could cause security issues and abuse by observers.

3. If we didn't use multi threading, without concurrency there will likely be a performance impact, processes may take longer to complete because it goes sequentially.