# Architecture (v1)

```mermaid
flowchart LR
    subgraph Sources
        A[iNaturalist / GBIF<br/>species observations]
        B[Open-Meteo / NWS<br/>weather]
        C[NLCD, 3DEP, NHD<br/>land cover, elevation, water]
    end

    subgraph Pipeline
        D[Scheduled ingestion<br/>Prefect]
        E[(Parquet + DuckDB)]
        F[H3 grid and<br/>feature tables]
    end

    subgraph Models
        G[Habitat suitability<br/>LightGBM, spatial CV]
        H[Activity model<br/>weather vs ideal conditions]
        I[MLflow<br/>experiment tracking]
    end

    subgraph Serving
        J[FastAPI]
        K[(Redis cache)]
        L[MapLibre heatmap<br/>1 / 5 / 10 mile radii]
    end

    A --> D
    B --> D
    C --> D
    D --> E --> F
    F --> G
    F --> H
    G --> I
    H --> I
    G --> J
    H --> J
    B -->|live weather| J
    J <--> K
    J --> L
```

## Score

Likelihood = P(suitable habitat) x P(active | current conditions)

## Notes
- Habitat scores are precomputed; only the weather layer refreshes hourly.
- Training uses a wider region than Heflin; predictions are served locally.
