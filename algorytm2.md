```mermaid
graph TD
    Start([START]) --> Wczytaj[/Wczytaj zbiór liczb/]
    Wczytaj --> CzyNieparzysta{Czy liczba elementów<br>jest nieparzysta?}
    
    %% Sciezka TAK (Nieparzyste)
    CzyNieparzysta -->|TAK| InitNieparzyste[MIN = element 0 <br> MAX = element 0 <br> i = 1]
    
    %% Sciezka NIE (Parzyste)
    CzyNieparzysta -->|NIE| CzyAmniejszeB{Czy element 0 <br> < element 1 ?}
    CzyAmniejszeB -->|TAK| InitParzysteTAK[MIN = element 0 <br> MAX = element 1]
    CzyAmniejszeB -->|NIE| InitParzysteNIE[MIN = element 1 <br> MAX = element 0]
    
    InitParzysteTAK --> UstawI2[i = 2]
    InitParzysteNIE --> UstawI2
    
    %% Polaczenie przed petla
    InitNieparzyste --> Petla{Czy i < n?}
    UstawI2 --> Petla
    
    %% Wnetrze petli
    Petla -->|TAK| PobierzPare[A = element i <br> B = element i+1]
    PobierzPare --> CzyAmniejszeB_Para{Czy A < B?}
    
    %% Podpetla dla A < B
    CzyAmniejszeB_Para -->|TAK| CzyAmniejszeMin{Czy A < MIN?}
    CzyAmniejszeMin -->|TAK| UstawMinA[MIN = A]
    CzyAmniejszeMin -->|NIE| CzyBwiekszeMax{Czy B > MAX?}
    UstawMinA --> CzyBwiekszeMax
    CzyBwiekszeMax -->|TAK| UstawMaxB[MAX = B]
    
    %% Podpetla dla A >= B
    CzyAmniejszeB_Para -->|NIE| CzyBmniejszeMin{Czy B < MIN?}
    CzyBmniejszeMin -->|TAK| UstawMinB[MIN = B]
    CzyBmniejszeMin -->|NIE| CzyAwiekszeMax{Czy A > MAX?}
    UstawMinB --> CzyAwiekszeMax
    CzyAwiekszeMax -->|TAK| UstawMaxA[MAX = A]
    
    %% Inkrementacja i powrot
    UstawMaxB --> Ink[i = i + 2]
    CzyBwiekszeMax -->|NIE| Ink
    UstawMaxA --> Ink
    CzyAwiekszeMax -->|NIE| Ink
    
    Ink ----> Petla
    
    %% Wyjscie z petli
    Petla -->|NIE| Wypisz[/Wypisz MIN, MAX/]
    Wypisz --> Stop([STOP])
