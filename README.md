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
