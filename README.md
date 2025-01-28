# Block 37 Many to Many Relations, Guided Practice: Table
Develop a backend to support functionality for customers to make reservations for a table at a restaurant of their choice.

## Getting Started

1. Create a new repository 
2. Configure your `.env` file. Use `table` as the name of the database for this activity.

## Initializing the Database

<figure>

![Visualized schema. The textual representation in DBML is linked below.](/docs/schema.svg)

<figcaption>

[textual representation of schema in DBML](/docs/schema.dbml)

</figcaption>
</figure>

1. Create the `Restaurant`, `Reservation`, and `Customer` models in the Prisma schema. Refer to the [Prisma docs on many-to-many relations](https://www.prisma.io/docs/orm/prisma-schema/data-model/relations/many-to-many-relations).

   - One Restaurant can have many Reservations.
   - There is an _implicit_ many-to-many relation between Reservations and Customers.
     - One Customer can have many Reservations.
     - One Reservation can have many Customers.
   - Reservation is the relation table for the _explicit_ many-to-many relation between Restaurants and Customers.

2. Create the initial migration with `npx prisma migrate dev`.

## Seeding the Database

Write the following code in the `seed` function.

1.  Create 3 restaurants.
2.  Create 5 customers.
3.  Read the [Prisma example on connecting a new record to multiple existing records](https://www.prisma.io/docs/orm/prisma-client/queries/relation-queries#connect-multiple-records).
4.  Create 8 reservations that are each connected to a single restaurant and multiple customers. In each iteration:

    1. Generate a random integer between 1 and 3, inclusive. This will be the number of customers in this reservation.
    2. Create an array of that length. It should be filled with objects. Each object should have an `id` key. The value of that key should be a random customer id.
    3. Create a new reservation with a random restaurant id. You can use an arbitrary date. Use the array you created to **connect** it to the corresponding customers.

## Adding a Reservation

The API for this activity will only serve one route, so there is no need for a separate router file. In `server.js`, add a handler for `POST /reservations`.

- The request body should include `date`, `restaurantId` and `customerIds`, which will be an array of numbers.
- A reservation should be created for the specific restaurant and _connected_ to the specified customers.
- Send the newly created reservation as a response with status 201. This should _include_ the restaurant and customers.
