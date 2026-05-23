```mermaid
graph TD
    Start([START]) --> Decyzja{Czy A < B?}
    Decyzja -->|TAK| BlokA[MIN = A]
    Decyzja -->|NIE| BlokB[MIN = B]
    BlokA --> Stop([STOP])
    BlokB --> Stop([STOP])
