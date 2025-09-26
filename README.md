    %% ----- Nodes -----
    subgraph Motor["Motor / Gearbox"]
        direction LR
        M1[Motor] --> G1[Gear Reduction]
    end

    subgraph Pin["Coupling Pin (axle)"]
        direction LR
        P1[Pin ►]:::lockedStyle
        P2[Pin ◄]:::unlockedStyle
    end

    subgraph Latch["Latch Mechanism"]
        direction LR
        L1[Latch Engaged]:::lockedStyle
        L2[Latch Released]:::unlockedStyle
    end

    subgraph Hall["Hall‑Sensor"]
        H[Hall Sensor]:::sensorStyle
    end

    subgraph Button["Micro‑Button"]
        B[NC / NO contacts]:::buttonStyle
    end

    %% ----- Connections -----
    Motor --> Pin
    Pin --> Latch
    Pin --> Hall
    Pin --> B

    %% ----- States -----
    classDef lockedStyle fill:#e6ffe6,stroke:#2c662d,color:#0b5300;
    classDef unlockedStyle fill:#ffe6e6,stroke:#992d2d,color:#660000;
    classDef sensorStyle fill:#e0f0ff,stroke:#0066cc,color:#003366;
    classDef buttonStyle fill:#fff4e6,stroke:#b38f00,color:#663d00;

    %% ----- Legends -----
    click Motor "https://technica-eng.com/docs/aag-motor" "Motor & driver"
    click Hall "https://technica-eng.com/docs/aag-hall" "Hall‑sensor spec"
    click Button "https://technica-eng.com/docs/aag-button" "Micro‑button spec"

    %% ----- State Labels -----
    LockedState[Locking (Locked) ]:::lockedStyle
    UnlockedState[Unlocking (Unlocked) ]:::unlockedStyle

    %% Position arrows
    LockedState -.-> P1
    LockedState -.-> L1
    LockedState -.-> B(NC closed)

    UnlockedState -.-> P2
    UnlockedState -.-> L2
    UnlockedState -.-> B(NO closed)

    %% Optional notes
    note top of LockedState
        • Pin fully re‑tracted<br/>
        • Latch mechanically engaged<br/>
        • Hall‑sensor count = LOCKED_HALL_COUNT<br/>
        • NC contact closed (0 V)
    end

    note top of UnlockedState
        • Pin fully extended<br/>
        • Latch released<br/>
        • Hall‑sensor count = UNLOCKED_HALL_COUNT<br/>
        • NO contact closed (0 V)
    end
