# Flowchart


## Basic Flow

graph TD
A([Start]) --> B{Is it working?}
B -->|Yes| C[Ship it]
B -->|No| D[Debug]
D --> E[Fix the issue]
E --> B
C --> F([Done])

## Left-Right

graph LR
A[Input] --> B[Process A]
A --> C[Process B]
B --> D{Merge?}
C --> D
D --> E[Output]

## Decision Tree

graph TD
A[User Login] --> B{Credentials valid?}
B -->|Yes| C{Has 2FA?}
B -->|No| F[Show error]
C -->|Yes| D[Request OTP]
C -->|No| E[Grant access]
D --> G{OTP correct?}
G -->|Yes| E
G -->|No| H[Block attempt]

## Sub Group

graph TB
subgraph Frontend
A[React App] --> B[API Client]
end
subgraph Backend


C[REST API] --> D[Business Logic]
D --> E[(Database)]
end
B --> C


# Sequence


## Basic Messages

sequenceDiagram
participant Alice
participant John
Alice->>John: Hello John, how are you?
John-->>Alice: Great!
Alice-)John: See you later!

## Activation

sequenceDiagram
Alice->>+John: Hello John, how are you?
Alice->>+John: John, can you hear me?
John-->>-Alice: Hi Alice, I can hear you!
John-->>-Alice: I feel great!

## Loop and Alt

sequenceDiagram
Alice->>Bob: Hello Bob, how are you?
alt is sick
Bob->>Alice: Not so good
else is well
Bob->>Alice: Feeling fresh like a daisy
end
opt Extra response
Bob->>Alice: Thanks for asking
end
loop Every minute
Alice-->>Bob: Are you OK?
end

## Parallel

sequenceDiagram
par Alice to Bob
Alice->>Bob: Hello guys!


and Alice to John
Alice->>John: Hello guys!
end
Bob-->>Alice: Hi Alice!
John-->>Alice: Hi Alice!

## Notes & Rect

sequenceDiagram
participant Alice
participant John
Note right of Alice: Alice calls John.
Alice->>+John: Hello John, how are you?
Alice->>+John: John, can you hear me?
John-->>-Alice: Hi Alice, I can hear you!
John-->>-Alice: I feel great!
Note over Alice,John: A typical interaction

## Actor Types

sequenceDiagram
participant API as Public API
participant Auth as Auth Service
participant DB as User Database
API->>Auth: Login request
Auth->>DB: Query user
DB-->>Auth: User data
Auth-->>API: Access token

## Create & Destroy

sequenceDiagram
Alice->>Bob: Hello Bob, how are you?
Bob->>Alice: Fine, thank you. And you?
create participant Carl
Alice->>Carl: Hi Carl!
destroy Carl
Alice-xCarl: We are too many
destroy Bob
Bob->>Alice: I agree


## Critical Region

sequenceDiagram
critical Establish a connection to the DB
Service-->DB: connect
option Network timeout
Service-->Service: Log error
option Credentials rejected
Service-->Service: Log different error
end

## Autonumber

sequenceDiagram
autonumber
Alice->>John: Hello John, how are you?
loop HealthCheck
John->>John: Fight against hypochondria
end
Note right of John: Rational thoughts!
John-->>Alice: Great!
John->>Bob: How about you?
Bob-->>John: Jolly good!


# Class Diagram


## Basic Class

classDiagram
Animal <|-- Duck
Animal <|-- Fish
Animal <|-- Zebra
Animal : +int age
Animal : +String gender
Animal : +isMammal()
Animal : +mate()
class Duck{
+String beakColor
+swim()
+quack()
}
class Fish{
-int sizeInFeet
-canEat()
}
class Zebra{
+bool is_wild
+run()
}

## Members & Visibility

classDiagram
class BankAccount{
+String owner
+BigDecimal balance
+deposit(amount) bool
+withdrawal(amount) int
+getHistory() List~Transaction~
+clearAccount() void
}
class Transaction{
+String id
+BigDecimal amount
+Date timestamp
+getDetails() String
}
BankAccount "1" --> "*" Transaction : records


## All Relation

classDiagram
classA <|-- classB : Inheritance
classC *-- classD : Composition
classE o-- classF : Aggregation
classG --> classH : Association
classI -- classJ : Link
classK ..> classL : Dependency
classM ..|> classN : Realization
classO .. classP : Dashed

## Inheritance Tree

classDiagram
class Shape{
<<interface>>
+draw() void
+getArea() float
}
class Circle{
+float radius
+draw() void
+getArea() float
}
class Rectangle{
+float width
+float height
+draw() void
+getArea() float
}
class Triangle{
+float base
+float height
+draw() void
+getArea() float
}
Shape <|.. Circle
Shape <|.. Rectangle
Shape <|.. Triangle


## Annotations

classDiagram
class Animal{
<<abstract>>
+String name
+makeSound() void
}
class Dog{
+fetch() void
}
class Cat{
+purr() void
}
class IPet{
<<interface>>
+getOwner() String
}
class PetType{
<<enumeration>>
DOG
CAT
BIRD
}
Animal <|-- Dog
Animal <|-- Cat
Dog ..|> IPet
Cat ..|> IPet

## Cardinality

classDiagram
class Customer{
+String name
+String email
}
class Order{
+String orderId
+getTotal() float
}
class Product{
+String name
+float price
}
Customer "1" --> "0..*" Order : places


Order "1" --> "1..*" Product : contains

## Namespace

classDiagram
namespace Shapes {
class Triangle{
+float base
+float height
}
class Rectangle{
+float width
+float height
}
}
namespace Utils {
class MathHelper{
+sqrt(n) float
+pow(b, e) float
}
}
Triangle --> MathHelper : uses
Rectangle --> MathHelper : uses

## Generic Types

classDiagram
class Stack~T~{
-List~T~ items
+push(item T) void
+pop() T
+isEmpty() bool
}
class Queue~T~{
-List~T~ items
+enqueue(item T) void
+dequeue() T
+isEmpty() bool
}
class Repository~T~{
<<interface>>
+findById(id String) T
+findAll() List~T~


+save(entity T) void
}

## Direction RL

classDiagram
direction RL
class Student {
-String name
+study() void
}
class IdCard{
-int id
-String name
+isValid() bool
}
class Bike{
-String model
+ride() void
}
Student "1" --> "1" IdCard : carries
Student "1" --> "1" Bike : rides


# State Diagram


## Basic State

stateDiagram-v
[*] --> Still
Still --> [*]
Still --> Moving
Moving --> Still
Moving --> Crash
Crash --> [*]

## Composite State

stateDiagram-v
[*] --> First
state First {
[*] --> second
second --> [*]
}
[*] --> NamedComposite
NamedComposite: Another Composite
state NamedComposite {
[*] --> namedSimple
namedSimple --> [*]
namedSimple: Another simple
}

## Choice

stateDiagram-v
state if_state <<choice>>
[*] --> IsPositive
IsPositive --> if_state
if_state --> False: if n < 0
if_state --> True: if n >= 0

## Fork & Join

stateDiagram-v
state fork_state <<fork>>


[*] --> fork_state
fork_state --> State
fork_state --> State
state join_state <<join>>
State2 --> join_state
State3 --> join_state
join_state --> State
State4 --> [*]

## Notes

stateDiagram-v
State1: The state with a note
note right of State
Important information!
You can write notes.
end note
State1 --> State
note left of State2: This is the note to the left.

## Concurrency

stateDiagram-v
[*] --> Active
state Active {
[*] --> NumLockOff
NumLockOff --> NumLockOn: EvNumLockPressed
NumLockOn --> NumLockOff: EvNumLockPressed
--
[*] --> CapsLockOff
CapsLockOff --> CapsLockOn: EvCapsLockPressed
CapsLockOn --> CapsLockOff: EvCapsLockPressed
--
[*] --> ScrollLockOff
ScrollLockOff --> ScrollLockOn: EvScrollLockPressed
ScrollLockOn --> ScrollLockOff: EvScrollLockPressed
}

## Direction LR

stateDiagram-v
direction LR


### [*] --> A

### A --> B

### B --> C

state B {
direction LR
a --> b
}
B --> D


# ER Diagram


## Basic ER

erDiagram
CUSTOMER ||--o{ ORDER : places
ORDER ||--|{ LINE-ITEM : contains
CUSTOMER }|..|{ DELIVERY-ADDRESS : uses

## With Attributes

erDiagram
CUSTOMER ||--o{ ORDER : places
CUSTOMER {
string name
string custNumber
string sector
}
ORDER ||--|{ LINE-ITEM : contains
ORDER {
int orderNumber
string deliveryAddress
}
LINE-ITEM {
string productCode
int quantity
float pricePerUnit
}

## Keys & Comment

erDiagram
CAR ||--o{ NAMED-DRIVER : allows
CAR {
string registrationNumber PK
string make
string model
}
PERSON ||--o{ NAMED-DRIVER : is
PERSON {
string driversLicense PK "The license number"
string firstName
string lastName
string phone UK
int age


### }

### NAMED-DRIVER {

string carRegistrationNumber PK,FK
string driverLicence PK,FK
}

## Identifying VS Not

erDiagram
CAR ||--o{ NAMED-DRIVER : allows
PERSON }o..o{ NAMED-DRIVER : is
CAR {
string registrationNumber
string make
string model
}
PERSON {
string firstName
string lastName
int age
}

## Entity Aliases

erDiagram
p[Person] {
string firstName
string lastName
}
a["Customer Account"] {
string email
string plan
}
p ||--o| a : has

## ER Direction LR

erDiagram
direction LR
CUSTOMER ||--o{ ORDER : places
CUSTOMER {
string name
string custNumber


string sector
}
ORDER ||--|{ LINE-ITEM : contains
ORDER {
int orderNumber
string deliveryAddress
}
LINE-ITEM {
string productCode
int quantity
float pricePerUnit
}


# User Journey


## Working Day

journey
title My working day
section Go to work
Make tea: 5: Me
Go upstairs: 3: Me
Do work: 1: Me, Cat
section Go home
Go downstairs: 5: Me
Sit down: 5: Me

## Online Shopping

journey
title Online Shopping Experience
section Discovery
Search for product: 5: Customer
Browse results: 4: Customer
Read reviews: 3: Customer
section Purchase
Add to cart: 5: Customer
Enter details: 2: Customer
Confirm order: 4: Customer
section Delivery
Receive confirmation: 5: Customer
Track package: 3: Customer
Receive item: 5: Customer

## User Onboarding

journey
title User Onboarding Flow
section Sign Up
Visit landing page: 4: User
Click sign up: 5: User
Fill in form: 2: User
Verify email: 3: User
section Getting Started
Complete profile: 3: User
Take product tour: 4: User, System
Try first feature: 4: User
section Activation


Invite team member: 3: User
Complete first task: 5: User
Receive achievement: 5: User, System


# Gantt


## Basic Gantt

gantt
title A Gantt Diagram
dateFormat YYYY-MM-DD
section Section
A task :a1, 2014-01-01, 30d
Another task :after a1, 20d
section Another
Task in Another :2014-01-12, 12d
another task :24d

## Full Syntax

gantt
dateFormat YYYY-MM-DD
title Adding GANTT diagram functionality to mermaid
excludes weekends
section A section
Completed task :done, des1, 2014-01-06, 2014-01-08
Active task :active, des2, 2014-01-09, 3d
Future task : des3, after des2, 5d
Future task2 : des4, after des3, 5d
section Critical tasks
Completed in crit line :crit, done, 2014-01-06, 24h
Implement parser :crit, done, after des1, 2d
Create tests :crit, active, 3d
Future crit task :crit, 5d
section Documentation
Describe gantt syntax :active, a1, after des1, 3d
Add gantt to demo page :after a1, 20h
Add another diagram :doc1, after a1, 48h
section Last section
Describe gantt syntax :after doc1, 3d
Add gantt to demo page :20h
Add another diagram :48h

## Milestone

gantt
dateFormat HH:mm
axisFormat %H:%M
Initial milestone : milestone, m1, 17:49, 2m


Task A : 10m
Task B : 5m
Final milestone : milestone, m2, 18:08, 4m

## Excludes Weekend

gantt
title A Gantt Diagram Excluding Weekends
dateFormat YYYY-MM-DD
excludes weekends
section Section
A task :a1, 2024-01-01, 30d
Another task :after a1, 20d

## Bar Chart Style

gantt
title Git Issues - days since last update
dateFormat X
axisFormat %s
section Issue19062
71 : 0, 71
section Issue19401
36 : 0, 36
section Issue193
34 : 0, 34
section Issue7441
9 : 0, 9
section Issue1300
5 : 0, 5


# Pie Chart


## Basic Pie

pie title Pets adopted by volunteers
"Dogs" : 386
"Cats" : 85
"Rats" : 15

## Show data values

pie showData
title Key elements in Product X
"Calcium" : 42.96
"Potassium" : 50.05
"Magnesium" : 10.01
"Iron" : 5

## Text Position

pie showData
title Browser Market Share 2024
"Chrome" : 65.12
"Safari" : 18.75
"Edge" : 5.43
"Firefox" : 3.08
"Other" : 7.62


# Quadrant Chart


## Campaign Chart

quadrantChart
title Reach and engagement of campaigns
x-axis Low Reach --> High Reach
y-axis Low Engagement --> High Engagement
quadrant-1 We should expand
quadrant-2 Need to promote
quadrant-3 Re-evaluate
quadrant-4 May be improved
Campaign A: [0.3, 0.6]
Campaign B: [0.45, 0.23]
Campaign C: [0.57, 0.69]
Campaign D: [0.78, 0.34]
Campaign E: [0.40, 0.34]
Campaign F: [0.35, 0.78]

## Priority Matrix

quadrantChart
title Priority Matrix
x-axis Low Effort --> High Effort
y-axis Low Impact --> High Impact
quadrant-1 Do Later
quadrant-2 Quick Wins
quadrant-3 Deprioritize
quadrant-4 Major Projects
Fix login bug: [0.2, 0.9]
Add dark mode: [0.5, 0.7]
Refactor DB: [0.8, 0.85]
Update docs: [0.15, 0.4]
New dashboard: [0.75, 0.6]
Fix typos: [0.1, 0.15]
API v2: [0.9, 0.95]

## No Points

quadrantChart
title Eisenhower Matrix
x-axis Urgent --> Not Urgent
y-axis Not Important --> Important
quadrant-1 Plan
quadrant-2 Do


quadrant-3 Delegate
quadrant-4 Delete

## Point Styling

quadrantChart
title Reach and engagement of campaigns
x-axis Low Reach --> High Reach
y-axis Low Engagement --> High Engagement
quadrant-1 We should expand
quadrant-2 Need to promote
quadrant-3 Re-evaluate
quadrant-4 May be improved
Campaign A: [0.9, 0.0] radius: 12
Campaign B:::class1: [0.8, 0.1] color: #ff3300, radius: 10
Campaign C: [0.7, 0.2] radius: 25, color: #00ff33, stroke-color: #10f0f0
Campaign D: [0.6, 0.3] radius: 15, stroke-color: #00ff0f, stroke-width: 5px
Campaign E:::class2: [0.5, 0.4]
Campaign F:::class3: [0.4, 0.5] color: #0000ff
classDef class1 color: #109060
classDef class2 color: #908342, radius: 10, stroke-color: #310085, stroke-width: 3px
classDef class3 color: #f00fff, radius: 10


# Git Graph


## Basic Commits

gitGraph
commit
commit
commit
commit

## Branch & Merge

gitGraph
commit
commit
branch develop
commit
commit
commit
checkout main
commit
commit
merge develop
commit
commit

## Commit Types

gitGraph
commit id: "Normal"
commit id: "Auto-1"
commit id: "Reverse" type: REVERSE
commit id: "Auto-2"
commit id: "Highlight" type: HIGHLIGHT
commit id: "Auto-3"

## Git Flow

gitGraph
commit id: "init"
branch develop
commit id: "dev-1"
branch feature/login


commit id: "login-1"
commit id: "login-2"
checkout develop
merge feature/login id: "merge-login"
commit id: "dev-2"
branch release/1.0
commit id: "rc-1"
checkout main
merge release/1.0 id: "v1.0.0" tag: "v1.0.0"
checkout develop
merge release/1.0
commit id: "dev-3"

## Tags & IDs

gitGraph
commit id: "initial" tag: "v0.1"
commit
branch develop
commit id: "feat-A" tag: "alpha"
commit id: "feat-B"
checkout main
commit id: "hotfix" type: REVERSE tag: "v0.1.1"
merge develop id: "release" tag: "v1.0.0"
commit type: HIGHLIGHT


# C4 Diagram


## System Context

C4Context
title System Context diagram for Online Shop
Person(customer, "Customer", "A user of the online shop")
Person_Ext(admin, "Admin", "Shop administrator")
System(shop, "Online Shop", "Allows customers to browse and purchase products")
System_Ext(payment, "Payment Gateway", "Handles payment processing")
System_Ext(email, "Email System", "Sends order confirmations")
Rel(customer, shop, "Uses")
Rel(admin, shop, "Manages")
Rel(shop, payment, "Processes payments via")
Rel(shop, email, "Sends emails via")

## Container

C4Container
title Container diagram for Online Shop
Person(customer, "Customer", "A user of the online shop")
System_Ext(payment, "Payment Gateway", "External payment processor")
Container_Boundary(c1, "Online Shop") {
Container(web, "Web App", "React", "Provides the shop UI")
Container(api, "API Server", "Node.js", "Handles business logic")
ContainerDb(db, "Database", "PostgreSQL", "Stores products and orders")
}
Rel(customer, web, "Uses", "HTTPS")
Rel(web, api, "Calls", "JSON/HTTPS")
Rel(api, db, "Reads/writes", "SQL")
Rel(api, payment, "Processes payment", "HTTPS")

## Component

C4Component
title Component diagram for API Server
Container(web, "Web App", "React", "The shop frontend")
ContainerDb(db, "Database", "PostgreSQL", "Stores data")
Container_Boundary(api, "API Server") {
Component(auth, "Auth Controller", "Express", "Handles login and sessions")
Component(catalog, "Catalog Controller", "Express", "Manages product listings")
Component(orders, "Order Controller", "Express", "Processes orders")
}
Rel(web, auth, "Authenticates via", "JSON/HTTPS")
Rel(web, catalog, "Fetches products from", "JSON/HTTPS")


Rel(web, orders, "Places orders via", "JSON/HTTPS")
Rel(auth, db, "Reads users from", "SQL")
Rel(catalog, db, "Reads products from", "SQL")
Rel(orders, db, "Writes orders to", "SQL")

## Dynamic

C4Dynamic
title Dynamic diagram for Login Flow
ContainerDb(db, "Database", "PostgreSQL", "Stores user credentials")
Container(web, "Web App", "React", "The shop frontend")
Container_Boundary(api, "API Server") {
Component(auth, "Auth Controller", "Express", "Handles login")
Component(security, "Security Service", "Node.js", "Validates credentials")
}
Rel(web, auth, "POST /login", "JSON/HTTPS")
Rel(auth, security, "validateUser()")
Rel(security, db, "SELECT * FROM users WHERE email = ?", "SQL")

## Deployment

C4Deployment
title Deployment diagram for Online Shop
Deployment_Node(cloud, "AWS Cloud", "Amazon Web Services") {
Deployment_Node(web_tier, "Web Tier", "EC2 Auto Scaling") {
Container(web, "Web App", "React", "Serves the frontend")
}
Deployment_Node(app_tier, "App Tier", "EC2 Auto Scaling") {
Container(api, "API Server", "Node.js", "Handles requests")
}
Deployment_Node(db_tier, "Database Tier", "RDS") {
ContainerDb(db, "Database", "PostgreSQL", "Stores all data")
}
}
Rel(web, api, "Makes API calls", "HTTPS")
Rel(api, db, "Reads and writes", "SQL")


# Mindmap


## Basic

mindmap
root((Mindmap))
Origins
Long history
Popularisation
Research
On effectiveness
On Automatic creation
Uses
Creative techniques
Strategic planning
Argument mapping
Tools
Pen and paper
Mermaid

## Shapes

mindmap
root((Circle root))
Square node
id1[I am a square]
id2[Another square]
Rounded node
id3(Rounded square)
id4(Another rounded)
Cloud node
id5)A cloud(
Bang node
id6))A bang((
Hexagon node
id7{{A hexagon}}

## Project Plan

mindmap
root((Project))
Planning
Define scope
Set timeline
Allocate budget


Design
Wireframes
Mockups
User testing
Development
Frontend
Backend
Database
Launch
QA testing
Deployment
Monitoring

## Study Notes

mindmap
root((Web Dev))
HTML
Structure
Semantic tags
Forms
CSS
Selectors
Flexbox
Grid
Animations
JavaScript
Variables
Functions
DOM manipulation
Async and Await
Frameworks
React
Vue
Angular


# Timeline


## Timeline Basic

timeline
title History of Social Media Platform
2002 : LinkedIn
2004 : Facebook
2005 : YouTube
2006 : Twitter
2007 : Tumblr
2008 : Instagram
2010 : Pinterest

## Multi-Event

timeline
title Key Events in AI History
1950 : Turing Test proposed
1956 : Dartmouth Conference : Term AI coined
1997 : Deep Blue beats Kasparov
2012 : AlexNet wins ImageNet
2016 : AlphaGo beats Lee Sedol : DeepMind breakthrough
2022 : ChatGPT released : Generative AI goes mainstream
2023 : GPT-4 launched : Multimodal AI emerges

## Sections

timeline
title Timeline of Industrial Revolution
section 17th-20th century
Industry 1.0 : Machinery : Water power : Steam power
Industry 2.0 : Electricity : Internal combustion engine : Mass production
Industry 3.0 : Electronics : Computers : Automation
section 21st century
Industry 4.0 : Internet : Robotics : Internet of Things
Industry 5.0 : Artificial intelligence : Big data : 3D printing

## Project Roadmap

timeline
title Product Launch Roadmap 2025
section Q1


January : Kickoff meeting : Team onboarding
February : Requirements gathering : Design sprint
March : Prototype ready : Stakeholder review
section Q2
April : Development phase 1
May : Development phase 2 : QA testing begins
June : Beta release : User testing
section Q3
July : Bug fixes : Performance tuning
August : Final QA : Documentation complete
September : Public launch : Marketing campaign


# ZenUML


## Basic Messages ZenUML

zenuml
title Basic Messages
// Async message (arrow)
Alice->Bob: Hello Bob, how are you?
// Sync message (method call)
Bob.reply() {
return "Feeling great!"
}
Alice->Bob: See you later!

## Nesting

zenuml
title Nested Calls
Client->API.handleRequest() {
API->AuthService.verify() {
return token
}
API->Database.query() {
return data
}
return response
}

## Conditions

zenuml
title Login Flow
Client->AuthService: login(username, password)
if(credentials_valid) {
AuthService->TokenService.generate() {
return token
}
AuthService->Client: 200 OK with token
} else {
AuthService->Client: 401 Unauthorized
}


## Loop

zenuml
title Retry Pattern
Client->API: fetchData()
while(retries > 0) {
API->Database: query()
if(success) {
return data
} else {
API->API: retries--
}
}
API->Client: response

## Try / Catch

zenuml
title Payment Processing
try {
Consumer->API: submitPayment()
API->PaymentGateway: chargeCard()
PaymentGateway->API: 200 OK
API->Consumer: paymentConfirmed()
} catch {
PaymentGateway->API: error
API->Consumer: paymentFailed()
} finally {
API->AuditLog: logTransaction()
}


# Sankey


## Sankey Basic Flow

sankey
%% source,target,value
Electricity grid,Over generation / exports,104.453
Electricity grid,Heating and cooling - homes,113.726
Electricity grid,H2 conversion,27.14

## Sankey Energy System

sankey
%% source,target,value
Coal,Thermal generation,75.571
Gas,Thermal generation,151.891
Nuclear,Thermal generation,839.978
Wind,Electricity grid,289.366
Solar PV,Electricity grid,59.901
Hydro,Electricity grid,6.995
Thermal generation,Electricity grid,525.531
Thermal generation,Losses,787.129
Electricity grid,Industry,342.165
Electricity grid,Heating and cooling - homes,113.726
Electricity grid,Road transport,37.797
Electricity grid,Losses,56.691

## Sankey Budget Flow

sankey
%% source,target,value
Revenue,Operations,400
Revenue,Marketing,150
Revenue,Research,100
Revenue,Administration,80
Revenue,Savings,70
Operations,Salaries,250
Operations,Infrastructure,100
Operations,Supplies,50
Marketing,Digital ads,90
Marketing,Events,60
Research,Product dev,70
Research,Innovation,30


# XY Chart


## Bar Chart

xychart
title "Monthly Sales"
x-axis [jan, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec]
y-axis "Revenue (in $)" 4000 --> 11000
bar [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]

## Line Chart

xychart
title "Website Traffic"
x-axis [Mon, Tue, Wed, Thu, Fri, Sat, Sun]
y-axis "Visitors" 0 --> 5000
line [1200, 1800, 2400, 2100, 3200, 4800, 4200]

## Bar + Line

xychart
title "Sales Revenue"
x-axis [jan, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec]
y-axis "Revenue (in $)" 4000 --> 11000
bar [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]
line [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]

## Horizontal

xychart horizontal
title "Product Performance"
x-axis [ProductA, ProductB, ProductC, ProductD, ProductE]
y-axis "Units Sold" 0 --> 500
bar [120, 340, 210, 450, 280]
line [120, 340, 210, 450, 280]


# Block Diagram


## Basic Blocks

block
columns 3
A B C
D["Wide block"]:2 E

## Shapes Blocks

block
columns 3
rect["Rectangle"]
round("Round edges")
stadium(["Stadium"])
space
cylinder[("Database")]
circle(("Circle"))
space
diamond{"Decision"}
hexagon{{"Hexagon"}}
space
asymm>"Asymmetric"]
dblcirc((("Double circle")))

## Nested Blocks

block
columns 1
db(("DB"))
arrow<[" "]>(down)
block:mid
columns 3
A
B["Wide block"]
C
end
space
D
mid --> D
C --> D
style B fill:#969,stroke:#333,stroke-width:4px


## System Architecture

block
columns 3
Frontend blockArrowId<[" "]>(right) Backend
space:2 down<[" "]>(down)
Disk left<[" "]>(left) Database[("Database")]
classDef front fill:#696,stroke:#333;
classDef back fill:#969,stroke:#333;
class Frontend front
class Backend,Database back


# Packet Diagram


## Basic Fields

packet
title Simple Packet
+8: "Version"
+8: "Type"
+16: "Length"
+32: "Identifier"
+32: "Data"

## TCP Packet

packet
title TCP Packet
0-15: "Source Port"
16-31: "Destination Port"
32-63: "Sequence Number"
64-95: "Acknowledgment Number"
96-99: "Data Offset"
100-105: "Reserved"
106: "URG"
107: "ACK"
108: "PSH"
109: "RST"
110: "SYN"
111: "FIN"
112-127: "Window"
128-143: "Checksum"
144-159: "Urgent Pointer"
160-191: "(Options and Padding)"
192-255: "Data (variable length)"

## UDP Packet

packet
title UDP Packet
+16: "Source Port"
+16: "Destination Port"
+16: "Length"
+16: "Checksum"
64-95: "Data (variable length)"


## IPv4 Header

packet
title IPv4 Header
0-3: "Version"
4-7: "IHL"
8-15: "DSCP/ECN"
16-31: "Total Length"
32-47: "Identification"
48-50: "Flags"
51-63: "Fragment Offset"
64-71: "TTL"
72-79: "Protocol"
80-95: "Header Checksum"
96-127: "Source IP Address"
128-159: "Destination IP Address"
160-191: "Options (if IHL > 5)"


# Kanban


## Basic Board

kanban
todo[Todo]
task1[Design landing page]
task2[Write unit tests]
inprogress[In Progress]
task3[Build API endpoints]
task4[Review pull requests]
done[Done]
task5[Setup CI pipeline]
task6[Deploy to staging]

## With Metadata

kanban
todo[Todo]
id1[Fix login bug]@{ ticket: BUG-101, assigned: 'alice', priority: 'Very High' }
id2[Update README]@{ assigned: 'bob', priority: 'Low' }
inprogress[In Progress]
id3[Refactor auth module]@{ ticket: DEV-204, assigned: 'alice', priority: 'High' }
review[In Review]
id4[Add dark mode]@{ ticket: DEV-198, assigned: 'carol', priority: 'Low' }
done[Done]
id5[Setup linter]@{ assigned: 'bob' }

## Full Workflow

kanban
backlog[Backlog]
b1[User profile page]
b2[Email notifications]
b3[Export to CSV]
todo[Todo]
t1[Password reset flow]
t2[Mobile responsive nav]
inprogress[In Progress]
p1[Search feature]@{ assigned: 'alice', priority: 'High' }
p2[Dashboard charts]@{ assigned: 'bob', priority: 'High' }
review[Code Review]
r1[API rate limiting]@{ assigned: 'carol' }
done[Done]
d1[User authentication]
d2[Database migrations]
d3[Payment integration]


## Priority Board

kanban
critical[Critical]
c1[Production outage fix]@{ priority: 'Very High', assigned: 'alice' }
c2[Security vulnerability]@{ priority: 'Very High', assigned: 'bob' }
high[High Priority]
h1[Performance bottleneck]@{ priority: 'High', assigned: 'carol' }
h2[Data export broken]@{ priority: 'High', assigned: 'alice' }
normal[Normal]
n1[UI polish pass]@{ priority: 'Low' }
n2[Update dependencies]@{ priority: 'Low' }
low[Low Priority]
l1[Refactor old tests]@{ priority: 'Very Low' }
l2[Update docs]@{ priority: 'Very Low' }


# Architecture


## Basic Services

architecture-beta
group api(cloud)[API Layer]
service db(database)[Database] in api
service disk1(disk)[Storage] in api
service disk2(disk)[Storage] in api
service server(server)[Server] in api
db:L -- R:server
disk1:T -- B:server
disk2:T -- B:db

## With Arrows

architecture-beta
group vpc(cloud)[VPC]
service internet(internet)[Internet]
service gateway(server)[Gateway] in vpc
service app(server)[App Server] in vpc
service db(database)[Database] in vpc
service storage(disk)[Storage] in vpc
internet:R --> L:gateway
gateway:R --> L:app
app:R --> L:db
app:B --> T:storage

## Junction

architecture-beta
service left_disk(disk)[Disk A]
service top_disk(disk)[Disk B]
service bottom_disk(disk)[Disk C]
service top_gateway(internet)[Gateway A]
service bottom_gateway(internet)[Gateway B]
junction junctionCenter
junction junctionRight
left_disk:R -- L:junctionCenter
top_disk:B -- T:junctionCenter
bottom_disk:T -- B:junctionCenter
junctionCenter:R -- L:junctionRight
top_gateway:B -- T:junctionRight
bottom_gateway:T -- B:junctionRight


## Nested Groups

architecture-beta
group public(cloud)[Public Zone]
group private(cloud)[Private Zone] in public
service lb(server)[Load Balancer] in public
service web(server)[Web Server] in private
service api(server)[API Server] in private
service db(database)[Database] in private
service cache(disk)[Cache] in private
lb:R --> L:web
web:R --> L:api
api:B --> T:db
api:R --> L:cache


# Radar Chart


## Basic Radar

radar-beta
axis A, B, C, D, E
curve c1["Series 1"]{1, 2, 3, 4, 5}
curve c2["Series 2"]{5, 4, 3, 2, 1}
curve c3["Series 3"]{3, 3, 3, 3, 3}
max 5
min 0

## Grades Compare

radar-beta
title Grades Comparison
axis m["Math"], s["Science"], e["English"]
axis h["History"], g["Geography"], a["Art"]
curve alice["Alice"]{85, 90, 80, 70, 75, 90}
curve bob["Bob"]{70, 75, 85, 80, 90, 85}
max 100
min 0

## Polygon Graticule

radar-beta
title Restaurant Comparison
axis food["Food Quality"], service["Service"], price["Price"]
axis ambiance["Ambiance"]
curve a["Restaurant A"]{4, 3, 2, 4}
curve b["Restaurant B"]{3, 4, 3, 3}
curve c["Restaurant C"]{2, 3, 4, 2}
curve d["Restaurant D"]{2, 2, 4, 3}
graticule polygon
max 5

## Skills Matrix

radar-beta
title Team Skills Matrix
axis js["JavaScript"], py["Python"], ux["UX Design"]
axis db["Databases"], cloud["Cloud"], sec["Security"]
curve dev["Dev Team"]{90, 70, 60, 80, 75, 65}
curve ops["Ops Team"]{50, 80, 40, 85, 95, 90}
curve design["Design Team"]{60, 40, 95, 50, 55, 45}
max 100


min 0
ticks 4


# Treemap


## Basic Treemap

treemap-beta
"Category A"
"Item A1": 10
"Item A2": 20
"Item A3": 15
"Category B"
"Item B1": 25
"Item B2": 30
"Category C"
"Item C1": 18
"Item C2": 12

## Hierarchical

treemap-beta
"Products"
"Electronics"
"Phones": 50
"Computers": 30
"Accessories": 20
"Clothing"
"Men's": 40
"Women's": 40
"Home & Garden"
"Furniture": 35
"Tools": 25

## Budget Data

treemap-beta
"Annual Budget"
"Engineering"
"Salaries": 500000
"Equipment": 80000
"Training": 30000
"Marketing"
"Advertising": 200000
"Events": 60000
"Operations"
"Infrastructure": 150000
"Supplies": 40000


## Org Structure

treemap-beta
"Company"
"Engineering"
"Frontend": 12
"Backend": 15
"DevOps": 6
"QA": 8
"Product"
"Design": 7
"Management": 5
"Business"
"Sales": 20
"Marketing": 10
"Support": 14


# Venn Diagram


## Basic 2-Set

venn-beta
title "Team Overlap"
set Frontend
set Backend
union Frontend,Backend["Shared APIs"]

## Triple Set

venn-beta
title "Skill Sets"
set A["Python"]
set B["JavaScript"]
set C["SQL"]
union A,B["Full Stack"]
union B,C["Web + Data"]
union A,C["Data Science"]
union A,B,C["All Skills"]

## With Text Nodes

venn-beta
title "Tech Stack"
set A["Frontend"]
set B["Backend"]
set C["DevOps"]
union A,B["Full Stack"]
union B,C["Cloud APIs"]
union A,C["CI/CD"]
union A,B,C["Platform"]

## Sized Sets

venn-beta
title "Market Share"
set A["Product A"]:30
set B["Product B"]:20
set C["Product C"]:10
union A,B["A & B"]:8
union B,C["B & C"]:4
union A,C["A & C"]:3
union A,B,C["All"]:2


