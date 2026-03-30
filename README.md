# Distributed E-Commerce Order Engine Hackathon
# Project Overview
This project simulates a real-world backend system for an e-commerce platform similar to Amazon or Flipkart. It is a menu-driven CLI application designed to handle complex backend challenges such as:

Multi-user interactions
Inventory consistency
Order lifecycle management
Payment failures & recovery
Concurrency control
Event-driven processing

The system ensures data consistency, fault tolerance, and scalability principles typically used in distributed systems.

# Features Implemented
🧩 Core Features

1. Product Management
Add new products with unique IDs
Prevent duplicate product entries
Update stock dynamically
View all available products
Ensures stock never becomes negative

3. Multi-User Cart System
Separate cart for each user
Add, remove, and update items
Cart synchronized with inventory
Prevent adding items beyond available stock

5. Real-Time Stock Reservation
Stock is reserved when added to cart
Released when removed from cart
Prevents overselling issues

7. Concurrency Simulation
Simulates multiple users accessing same product
Implements logical locking mechanism
Ensures only one user can reserve limited stock

9. Order Placement Engine
Converts cart → order
Steps include:
Cart validation
Total calculation
Stock locking
Order creation
Cart clearing
Fully atomic transaction (all-or-nothing)

11. Payment Simulation
Random success/failure simulation
If payment fails:
Order is cancelled
Stock is restored

12. Transaction Rollback System
Ensures system consistency
On failure:
Undo stock reservation
Delete order
Restore system state

13. Order State Machine
Valid states:
CREATED → PENDING_PAYMENT → PAID → SHIPPED → DELIVERED
                      ↘ FAILED
                      ↘ CANCELLED
Prevents invalid state transitions
Maintains correct lifecycle flow

14. Discount & Coupon Engine
Auto discounts:
₹1000+ → 10% off
Quantity > 3 → extra 5%
Coupon codes:
SAVE10 → 10% off
FLAT200 → ₹200 off
Prevents invalid combinations

15. Inventory Alert System
Displays low stock products
Blocks purchase if stock = 0

16. Order Management
View all orders
Search by Order ID
Filter:
Completed
Cancelled
Failed

17. Order Cancellation Engine
Cancel active orders
Automatically restores stock
Prevents duplicate cancellation

18. Return & Refund System
Supports partial returns
Updates:
Inventory
Order total

19. Event-Driven System
Simulated event queue:
ORDER_CREATED
PAYMENT_SUCCESS
INVENTORY_UPDATED
Events executed in sequence
Failure stops next events

20. Inventory Reservation Expiry
Reserved stock auto-expires after time
Prevents cart hoarding

21. Audit Logging System
Immutable logs for all actions
Example:
[Time] USER_1 added PRODUCT_2 qty=3
[Time] ORDER_101 created

22. Fraud Detection System
Flags users if:
3 orders within 1 minute
High-value transactions
Helps simulate security layer

23. Failure Injection System
Random failures introduced in:
Payment
Order creation
Inventory update
Tests system robustness

24. Idempotency Handling
Prevents duplicate orders
Handles multiple clicks on "Place Order"

25. Microservice Simulation
Modules:
Product Service
Cart Service
Order Service
Payment Service

Benefits:
Loose coupling
Clean architecture
Better scalability

# Design Approach
🔹 Architecture Style
Modular design (microservice-inspired)
Separation of concerns:
Product handling
Cart management
Order processing
Payment simulation
User (CLI)
   ↓
Controller Layer (Menu / Input Handler)
   ↓
Service Layer
   ├── Product Service
   ├── Cart Service
   ├── Order Service
   ├── Payment Service
   ├── Inventory Service
   └── Logging & Fraud Service
   ↓
Data Layer (In-Memory Storage)
   ├── Products
   ├── Users / Carts
   ├── Orders
   ├── Logs
   └── Event Queue
   
🔹 Key Concepts Used
Concurrency Control
Locks for stock updates
Atomic Transactions
Ensures all steps succeed or rollback
Event-Driven Processing
Queue-based execution
State Machine
Order lifecycle validation
Fault Tolerance
Rollback & recovery mechanisms
Idempotency
Prevent duplicate operations

# Assumptions
CLI-based system (no UI/frontend)
In-memory storage (no database)
Single machine simulation of distributed system
Payment gateway is mocked (random success/failure)
Time-based expiry is simulated using timestamps
Users are identified by unique usernames

# How to Run the Project
🔧 Requirements
1. Python 3.x installed on your system
2. Download or clone the repository:
   git clone <your-repo-link>

3. Navigate to project folder:
   cd ecommerce_engine

4. Run the program:
   python hackthon.py

5. Use the menu options to interact with the system
