# Herpefauna Heatmap

A real-time heatmap estimating the likelihood that a supported reptile or amphibian is active in an area, shown at 1, 5, and 10 mile radii. It combines a habitat suitability model with a weather-driven activity model.

**First supported species:** Eastern Box Turtle (*Terrapene carolina carolina*)
**Study area:** Heflin, Alabama (Cleburne County) | **Status:** Sprint 1 (setup)

## Approach
Likelihood = P(suitable habitat) x P(active | current conditions)

1. **Habitat suitability:** presence-only model using iNaturalist/GBIF observations, land cover, elevation, and distance to water, validated with spatial block cross-validation.
2. **Activity:** current and recent weather compared with each species' ideal conditions, first rule-based, then ML.
3. **Serving:** H3 hex grid, FastAPI backend, MapLibre frontend.

## Repo layout
- `src/` application and pipeline code
- `notebooks/` exploration and spikes
- `tests/` automated tests
- `docs/` architecture, decisions, model cards, retros
- `data/` local data (git-ignored)

## Workflow
Work is tracked in Jira (Scrum, 2-week sprints). Branches and commits start with the ticket key. See `docs/definition_of_done.md`.

## Responsible use
Precise locations of sensitive species are never displayed. Scores indicate activity likelihood only, not a guarantee of sightings. Do not collect or disturb wildlife.
