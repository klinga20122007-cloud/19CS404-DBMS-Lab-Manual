# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1332" height="817" alt="seniero_1 drawio" src="https://github.com/user-attachments/assets/42bc280f-acb4-4a10-8c9f-05017570cecd" />

### Entities and Attributes

| Entity                        | Attributes (PK, FK)                                                            | Notes                                                |
| ----------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **Member**                    | **member_id (PK)**, name, membership_type, start_date                          | Stores gym member details                            |
| **Program**                   | **program_id (PK)**, program_name, duration                                    | Stores fitness program details                       |
| **Trainer**                   | **trainer_id (PK)**, trainer_name, specialization                              | Stores trainer information                           |
| **Personal_Training_Session** | **session_id (PK)**, member_id (FK), trainer_id (FK), session_date, attendance | Records personal training sessions booked by members |
| **Membership_Payment**        | **payment_id (PK)**, member_id (FK), amount, payment_date, payment_type        | Stores membership and session payment details        |



### Relationships and Constraints

| Relationship                                   | Cardinality | Participation | Notes                                                                                     |
| ---------------------------------------------- | ----------- | ------------- | ----------------------------------------------------------------------------------------- |
| Member **JOINS** Program                       | M : N       | Partial       | A member can join multiple programs, and a program can have multiple members.             |
| Trainer **ASSIGNED TO** Program                | M : N       | Partial       | A trainer may be assigned to multiple programs, and a program may have multiple trainers. |
| Member **BOOKS** Personal Training Session     | 1 : M       | Partial       | A member can book many sessions, but each session belongs to one member.                  |
| Trainer **CONDUCTS** Personal Training Session | 1 : M       | Partial       | A trainer can conduct many sessions, but each session is conducted by one trainer.        |
| Member **MAKES** Membership Payment            | 1 : M       | Total         | A member can make multiple payments, and every payment belongs to one member.             |


### Assumptions
- Each personal training session is conducted by exactly one trainer and booked by exactly one member.
- Attendance is recorded only for personal training sessions.
- Payments are linked to a single member and may include membership fees or personal training session charges.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1032" height="842" alt="Senieor_2 drawio" src="https://github.com/user-attachments/assets/c636fa42-5968-43b5-8b2f-88f661de7907" />

### Entities and Attributes


| Entity      | Attributes (PK, FK)                            | Notes                                                                  |
| ----------- | ---------------------------------------------- | ---------------------------------------------------------------------- |
| **Member**  | **member_id (PK)**, name, phone                | Stores library member details.                                         |
| **Book**    | **book_id (PK)**, title, author, category      | Stores information about books available in the library.               |
| **Loan**    | **loan_id (PK)**, loan_date, return_date, fine | Records book borrowing and return details.                             |
| **Event**   | **event_id (PK)**, event_name, event_date      | Stores details of library events.                                      |
| **Speaker** | **speaker_id (PK)**, speaker_name              | Stores information about event speakers/authors.                       |
| **Room**    | **room_id (PK)**, room_name, capacity          | Stores information about library rooms used for events and study_**_** |


### Relationships and Constraints

| Relationship               | Cardinality | Participation | Notes                                                                                |
| -------------------------- | ----------- | ------------- | ------------------------------------------------------------------------------------ |
| Member **BORROWS** Loan    | 1 : M       | Partial       | A member can borrow many books over time, creating multiple loan records.            |
| Book **LOANED** Loan       | 1 : M       | Partial       | A book can appear in many loan records over time, but each loan refers to one book.  |
| Member **REGISTERS** Event | M : N       | Partial       | A member can register for multiple events, and an event can have many members.       |
| Event **HAS** Speaker      | M : N       | Total         | An event has one or more speakers, and a speaker may participate in multiple events. |
| Room **HOSTS** Event       | 1 : M       | Partial       | A room can host many events over time, while each event is held in one room.         |


### Assumptions
- Overdue fines are recorded in the Loan entity.
- Each event is conducted in one room, but a room can host multiple events at different times.
- A member can borrow the same book multiple times on different loan dates.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1072" height="892" alt="seniero_3 drawio" src="https://github.com/user-attachments/assets/a3c6ed25-e6e9-4221-b438-a432ac197863" />

### Entities and Attributes


| Entity          | Attributes (PK, FK)                                                           | Notes                                         |
| --------------- | ----------------------------------------------------------------------------- | --------------------------------------------- |
| **Customer**    | **customer_id (PK)**, name, phone                                             | Stores customer details.                      |
| **Table**       | **table_id (PK)**, capacity                                                   | Stores restaurant table information.          |
| **Reservation** | **reservation_id (PK)**, reservation_date, reservation_time, number_of_guests | Stores reservation details.                   |
| **Order**       | **order_id (PK)**, order_time                                                 | Stores food orders placed for a reservation.  |
| **Dish**        | **dish_id (PK)**, dish_name, category, price                                  | Stores menu item details.                     |
| **Bill**        | **bill_id (PK)**, food_charge, service_charge, total_amount                   | Stores billing information for a reservation. |
| **Waiter**      | **waiter_id (PK)**, waiter_name                                               | Stores waiter details.                        |


### Relationships and Constraints

| Relationship                       | Cardinality | Participation | Notes                                                                                         |
| ---------------------------------- | ----------- | ------------- | --------------------------------------------------------------------------------------------- |
| Customer **MAKES** Reservation     | 1 : M       | Partial       | A customer can make multiple reservations, but each reservation belongs to one customer.      |
| Table **RESERVED FOR** Reservation | 1 : M       | Partial       | A table can be reserved many times at different times, but each reservation is for one table. |
| Reservation **HAS** Order          | 1 : M       | Partial       | A reservation may have multiple food orders, and each order belongs to one reservation.       |
| Order **CONTAINS** Dish            | M : N       | Total         | An order contains multiple dishes, and a dish can appear in multiple orders.                  |
| Reservation **GENERATES** Bill     | 1 : 1       | Total         | Each reservation generates one bill, and each bill belongs to one reservation.                |
| Waiter **SERVES** Reservation      | 1 : M       | Partial       | A waiter can serve multiple reservations, while each reservation is served by one waiter.     |


### Assumptions
- Walk-in customers are also recorded as customers before placing orders.
- Each reservation is assigned to one table and generates one final bill.
- A dish can appear in multiple orders, and an order can contain multiple dishes.


---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
