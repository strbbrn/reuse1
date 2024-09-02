```mermaid
graph TD;
    %% Pull Request Workflow
    A[Pull Request Event (synchronize, open, reopen, edited)] --> B[Trigger PR Checks Workflow];
    B --> C[Commit Linting];
    B --> D[Linting];
    B --> E[SCA Scan];
    B --> F[SonarQube];
    B --> G[Unit Test];
    C --> H{All Checks Passed?};
    D --> H;
    E --> H;
    F --> H;
    G --> H;
    H --> |Yes| I[Allow Merge];
    H --> |No| J[Block Merge];

    %% Push to Develop Branch Workflow
    K[Push to develop Branch] --> L[Trigger Build and Deploy Workflow];
    L --> M[Build];
    M --> N[Release Versioning];
    N --> O[Tag and Release Creation];
    O --> P[Deploy to Dev Environment];
    P --> Q[Dev Environment Health Check];
    Q --> R{Health Check Passed?};
    R --> |Yes| S[Skip Rollback];
    R --> |No| T[Rollback to Previous Release];

    %% Push to Main Branch Workflow
    U[Push to main Branch] --> V[Trigger Build and Deploy Workflow];
    V --> W[Check Previous Deployment Status];
    W --> X[Check Dev Environment Health];
    X --> Y{Checks Passed?};
    Y --> |Yes| Z[Deploy to Prod];
    Y --> |No| T;
    Z --> AA[Prod Environment Health Check];
    AA --> AB{Prod Health Check Passed?};
    AB --> |Yes| S;
    AB --> |No| T;
