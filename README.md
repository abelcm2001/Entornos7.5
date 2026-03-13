# Entornos7.5

Tarea 1

```mermaid

flowchart LR

Partner[Partner]
Administrator[Administrator]

subgraph Partner and administrator use case diagram

%% Declaración
login((login))
viewClasses((viewAvailableClasses))
reserveClass((reserveClass))
joinWaitingList((joinWaitingList))
createClass((createClass))
cancelSession((cancelSession))

%% Relaciones
viewClasses -.->|&lt;&lt;include&gt;&gt;| login
reserveClass -.->|&lt;&lt;include&gt;&gt;| login
joinWaitingList -.->|&lt;&lt;extend&gt;&gt;| reserveClass

end

%% Enlaces actor-caso de uso
Partner --> viewClasses
Partner --> reserveClass

Administrator --> createClass
Administrator --> cancelSession

```

Tarea 2.

```mermaid

sequenceDiagram

actor Partner
participant WebInterface
participant ReservationManager
participant Database

Partner->>WebInterface: confirmReservation
WebInterface->>ReservationManager: requestReservation

ReservationManager->>Database: checkAvailability
Database-->>ReservationManager: availabilityResult

alt spots available

ReservationManager->>Database: saveReservation
Database-->>ReservationManager: success
ReservationManager-->>WebInterface: reservationConfirmed
WebInterface-->>Partner: showSuccessMessage

else no spots available

ReservationManager->>Database: addToWaitingList
ReservationManager-->>WebInterface: waitingListNotification
WebInterface-->>Partner: showWaitingListMessage

end

```

Tarea 3

```mermaid

flowchart LR

Partner[Partner]
App[GymApp / Interface]
BookingSystem[BookingSystem]
GroupClass[GroupClass]
Database[Database]

Partner -- 1: requestBooking --> App
App -- 1.1: checkAvailability --> BookingSystem
BookingSystem -- 1.1.1: getAvailableSpots --> GroupClass
GroupClass -- 1.1.2: availableSpots --> BookingSystem
BookingSystem -- 1.2: saveBooking --> Database
BookingSystem -- 1.3: confirmBooking --> App
App -- 2: showConfirmation --> Partner

```

```mermaid

Tarea 4

flowchart TD

Start((Start))

A[Receive booking request]

B{Membership fee paid?}

C{Spots available?}

D[Block spot]

E[Send confirmation email]

End((End))

Start --> A
A --> B

B -- Yes --> C
B -- No --> End

C -- Yes --> D
C -- No --> End

D --> E
E --> End

```
