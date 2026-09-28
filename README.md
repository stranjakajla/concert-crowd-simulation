# Concert Crowd Evacuation Simulation

An **agent-based simulation** built in **NetLogo** that models crowd behavior at a concert and the evacuation after it ends. Each person is an agent with their own age, gender, body mass, speed, vision and stress level. The model tracks congestion at exits, panic, injuries and stampede casualties, and shows how factors like the number of exits, obstacles and crowd size affect evacuation safety.

## How it works

### 1. Concert phase

- People gather on the floor in front of the stage and move around slightly.
- Some visitors feel unwell and **leave early**. Others nearby step aside to let them pass.

### 2. Evacuation phase

When the concert ends, everyone heads for the nearest exit.

- **Pathfinding:** a breadth-first search (BFS) computes each patch's distance to the nearest exit, and agents follow the shortest path around walls and obstacles.
- **Crowd physics:** agents keep their distance from others (social-force-style repulsion) and try to free themselves when stuck.
- **Stress and panic:** stress grows during evacuation (the color changes from yellow through orange to red). In dense crowds, panic level rises (0–3) and people move faster.
- **Injuries:** in high density under panic, agents can get injured and slow down considerably.
- **Stampede casualties:** the crush force on a patch (sum of mass × speed) is compared with each person's health threshold, and exceeding it leads to death.

### Agent demographics

| Group | Share | Characteristics |
|---|---|---|
| Children | 15% | low mass, lower vision, lower health threshold |
| Adults | 70% | highest mass and health threshold, best vision |
| Elderly | 15% | slowest movement, lower health threshold |

Gender affects mass and health threshold. All results are also tracked by age group and gender.

## Parameters (Interface)

| Parameter | Description |
|---|---|
| `ukupno-prisutnih` | Number of people at the concert (up to 1500) |
| `concert-duration` | Concert length in ticks, before evacuation starts |
| `prosjecna-brzina-kretanja` | Average movement speed |
| `broj-izlaza` | Number of exits (2 or 3) |
| `add-obstacles` | Adds obstacles to the space (next to the stage and in the lower part of the room) |
| `nivo-stresa-za-paniku` | Stress level at which panic begins |
| `panic-mode` | Forces panic for everyone |
| `sansa-za-povredu` | Chance of injury in a crush |
| `sansa-za-smrt (%)` | Additional independent chance of death |
| `sansa-za-nelagodu` | Share of people who feel unwell and leave early |
| `show-heatmap` | Shows a crowd density heatmap |

## Measured results

- Evacuation time and efficiency
- Number of early exits, and exits used (left or right)
- Number of injured and dead over time, by age group and gender
- Maximum crowd density and the moment of peak density
- Bottleneck detection at exits and flow rate (people exiting per 50 ticks)

Plots in the interface: **Evacuation** (people remaining vs. exited), **Injured over time** and **Dead over time**. A detailed report is printed to the Command Center when the simulation ends.

## How to run

1. Install [NetLogo](https://www.netlogo.org/download/) **7.0** or newer. The `.nlogox` format is not supported by older versions.
2. Open `crowd_simulation.nlogox`.
3. Set the parameters, click **Setup**, then **Go**.

## Technologies

`NetLogo 7` · agent-based modeling · BFS pathfinding

## Author

Ajla Stranjak
