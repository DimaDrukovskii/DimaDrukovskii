# Delivery Grodno — Route Optimization Prototype

**Type:** Hackathon logistics / vehicle-routing prototype  
**Status:** Prototype and demonstrable optimization workflow; not a production delivery platform.  
**Source:** Private repository.

## Problem

A dispatcher needs to assign orders to a fleet while respecting vehicle capacity, delivery time windows, unloading time, and driver shift limits. Simply sorting orders by distance does not solve the constrained routing problem.

## What the prototype does

- Accepts orders and vehicle data.
- Builds road-distance and travel-time matrices with OSRM.
- Uses VROOM to optimize vehicle routes.
- Checks capacity, delivery windows, unloading, and shift constraints.
- Produces route plans, utilization, cost, and unassigned-order information.
- Provides a dispatcher interface built with React and Leaflet.

## Architecture

```text
Orders + Vehicles
       |
       v
Input validation / schemas
       |
       v
OSRM road matrix
       |
       v
VROOM optimizer
       |
       v
Constraint validation + metrics
       |
       v
Dispatcher map / route plan
```

## Engineering competencies demonstrated

- Modeling a constrained vehicle-routing problem.
- Integrating an external routing engine and road-network service.
- Backend API and data-contract design.
- Fallback behavior when OSRM is unavailable.
- Separation of optimization, validation, persistence, and UI.
- End-to-end demo workflow.

## Reproducible demo

```bash
python -m pip install -r backend/requirements-pyvroom.txt
python scripts/plan_demo.py --matrix offline --out data/demo/plan_pyvroom.json
```

The offline matrix is an approximation and the generated plan is marked accordingly. For road-network-based results, use the OSRM-backed path.

## Stack

Python · FastAPI · SQLite · OSRM · VROOM / pyvroom · React · Leaflet · Docker

## Limitations

The repository describes this as a hackathon prototype / agreed framework rather than a ready-to-deploy application. Authentication, GPS tracking, a production mobile app, warehouse automation, and operational rollout are outside the current scope.
