# Collaborative Autonomous Cars Simulation

A multi-vehicle traffic simulation that explores how autonomous cars can share road-hazard information and coordinate safer driving decisions.

Built with Python and Pygame, the simulation places autonomous vehicles on a configurable multi-lane road. Vehicles detect potholes, react to changing weather, communicate hazards to nearby cars, and evaluate lane changes using safety, efficiency, and comfort scores.

## Highlights

- Multiple autonomous vehicles with visible IDs
- Cooperative vehicle-to-vehicle hazard sharing
- Pothole detection and avoidance
- Dynamic rain with reduced speed, visibility, and traction
- Safety-aware lane-change decisions
- Reactions to slower vehicles and surrounding traffic
- Weighted vehicle “happiness” scoring
- Smooth movement and lane-change animations
- A live event log for weather, hazards, and driving decisions
- Pause, step-forward, and step-back simulation controls
- Configurable road, traffic, weather, and scoring parameters

## How it works

Each vehicle continuously observes the road ahead and decides whether to remain in its lane or merge into a safer one. Decisions consider:

- Distance to nearby vehicles
- Relative vehicle speeds
- Potholes and rain in the current or adjacent lanes
- Safe merging distance
- Recent lane changes
- The vehicle's current happiness score

The happiness score combines three factors:

```text
happiness = safety × 5 + efficiency × 3 + comfort × 2
```

The highest-scoring vehicle becomes the highlighted ego vehicle. When it detects a hazard, it broadcasts that information to nearby vehicles, allowing them to plan before they encounter the hazard themselves.

## Requirements

- Python 3.8 or later
- [Pygame](https://www.pygame.org/)

## Installation

Clone the repository:

```bash
git clone https://github.com/MahianK/Collaborative-Autonomous-Cars-Simulation.git
cd Collaborative-Autonomous-Cars-Simulation/CCNY_Senior_Project_2
```

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell, activate it with:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Install Pygame:

```bash
python -m pip install pygame
```

## Running the simulation

Run the program from the `CCNY_Senior_Project_2` directory so it can find `config.txt` and the vehicle images:

```bash
python collaborative_autonomous_vehicles.py
```

## Controls

| Input | Action |
| --- | --- |
| `Space` | Pause or resume the simulation |
| `Right Arrow` | Advance one logic step while paused |
| `Left Arrow` | Restore the previous state while paused |
| Close window | Exit the simulation |

## Visual guide

- The distinct vehicle sprite marks the current ego vehicle.
- The number drawn on each vehicle is its unique ID.
- A pulsing warning icon shows that a vehicle is reacting to a hazard.
- Brown road marks represent potholes.
- Blue road marks and falling droplets indicate rain.
- The panel on the right displays recent simulation events.
- `R0`, `R1`, and similar labels identify grid rows; `C0` through `C3` identify lanes.

## Configuration

Simulation settings live in `CCNY_Senior_Project_2/config.txt`.

| Setting | Default | Description |
| --- | ---: | --- |
| `ROWS` | `300` | Length of the simulated road in grid cells |
| `COLS` | `4` | Number of lanes |
| `CELL_SIZE` | `40` | Size of each grid cell in pixels |
| `FPS` | `60` | Rendering frame rate |
| `VIEW_ROWS` | `25` | Number of visible road rows |
| `POTHOLE_CHANCE` | `5` | Base probability used when generating potholes |
| `WEATHER_CHANGE_CHANCE` | `2` | Per-update probability that rain begins |
| `RAIN_DURATION` | `20` | Number of logic updates for which rain persists |
| `NUM_CARS_SPAWN` | `4` | Number of vehicles created at startup |
| `MIN_VEHICLE_DISTANCE` | `8` | Reserved minimum vehicle-spacing setting |
| `MAX_VEHICLE_DISTANCE` | `15` | Maximum randomized starting offset |
| `VEHICLE_SPAWN_CHANCE` | `5` | Reserved for dynamic vehicle spawning |
| `SAFETY_WEIGHT` | `5.0` | Safety contribution to happiness |
| `EFFICIENCY_WEIGHT` | `3.0` | Efficiency contribution to happiness |
| `COMFORT_WEIGHT` | `2.0` | Comfort contribution to happiness |
| `ANIMATION_STEPS` | `10` | Render frames used to smooth each logic step |
| `LANE_CHANGE_COOLDOWN` | `5` | Delay before another lane change is allowed |

Some values in the configuration file are placeholders for planned behavior and are not yet used by the current simulation logic.

## Project structure

```text
Collaborative-Autonomous-Cars-Simulation/
├── README.md
└── CCNY_Senior_Project_2/
    ├── collaborative_autonomous_vehicles.py  # Simulation and rendering logic
    ├── config.txt                             # Tunable simulation parameters
    └── pngs/
        ├── car.png                            # Standard vehicle sprite
        └── car_ego.png                        # Ego-vehicle sprite
```

## Main components

### `Vehicle`

Models vehicle state and behavior, including movement, hazard detection, cooperative broadcasts, safe merging, animation, and happiness scoring.

### `Environment`

Owns the road grid, vehicles, faults, weather state, event history, updates, and rendering.

### Main loop

Processes keyboard input, stores snapshots for step-back behavior, advances simulation logic, selects the ego vehicle, and redraws the scene.

## Development check

You can verify the Python source without opening the Pygame window:

```bash
python -m py_compile collaborative_autonomous_vehicles.py
```

## Current limitations

- Dynamic vehicle spawning is currently disabled.
- Vehicles are initialized once and do not respawn after leaving the road.
- The model is a visual research simulation, not a physics-accurate or production autonomous-driving system.
- Ice-related configuration is present, but ice behavior is not implemented.
- Several safety distances are currently defined in the Python source rather than read from `config.txt`.

## Ideas for future work

- Add live controls for traffic and weather conditions
- Move all behavior constants into the configuration file
- Add collision, near-miss, and travel-time metrics
- Export experiment results for later analysis
- Support repeatable scenarios with configurable random seeds
- Add more road hazards and vehicle communication strategies
- Compare cooperative behavior against a non-communicating baseline
- Add automated tests for scoring and lane-change decisions

## Authors

- [@Msierra001](https://github.com/Msierra001)
- [@MKhan104](https://github.com/MKhan104)

## License

No license is currently included with this repository. Unless a license is added, the repository's contents remain under the copyright of their respective owner(s).
