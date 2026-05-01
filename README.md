# Grid Navigation Agent | AI Search Algorithms 🏠🌊

An AI-based grid navigation agent that finds the safest route through a flood-affected 
city using Greedy Best-First Search and Genetic Algorithm. Built on an 8×8 grid with 
dynamic scoring based on adjacent water bodies and flooded roads. Implemented in Python.

---

## 🧩 Problem Statement

During Cyclone Michaung in Nellore, Andhra Pradesh, most city areas are inundated with 
water. The agent navigates an 8×8 grid from a user-selected start state to a goal state 
while:
- Avoiding water bodies (`W`) and flooded roads (`F`) as blockades
- Maximizing a safety score based on adjacent cell types
- Minimizing the number of squares traversed
- Moving only Up, Down, Left, or Right (no diagonals)

### Scoring Rules
| Adjacent Cell Type | Score Impact |
|--------------------|-------------|
| Safe / Empty cell  | +5 points   |
| Water body         | −5 points   |
| Flooded road       | −3 points   |

---

## 🗺️ Grid Representation
. = Empty / Safe cell 

W = Water body (blockade) 

F = Flooded road (blockade)

The 8×8 grid is fully observable. Start and goal states are selected dynamically 
from all valid (non-blocked) cells.

---

## 🤖 Algorithms Implemented

### 1. Greedy Best-First Search
- Uses a **heuristic** — Manhattan distance normalized by the cell's transition cost
- Greedily expands the node with the lowest heuristic value
- Tracks expanded nodes, generated nodes, and max queue length for complexity analysis
- Fast and efficient with low time and space overhead

### 2. Genetic Algorithm
- Uses a **fitness function** — cumulative heuristic score across path nodes
- Evolves a population of candidate paths via:
  - **Tournament Selection** — picks best from a random sample
  - **Crossover** — combines two parent paths at a common grid point
  - **Mutation** (rate: 0.1) — replaces a sub-path between two random nodes
- Terminates early if fitness doesn't improve over 25 consecutive generations
- Explores a broader solution space at the cost of higher execution time

---

## ⚙️ Dynamic Input

The notebook supports dynamic start and goal state selection. On execution, all valid 
(non-blocked) grid cells are listed, and the user selects the start and end states by 
index.

Example run:
Start State: (0, 3)
Goal State:  (7, 4)
---

## 📊 Results (Sample Run)

Both algorithms found the same optimal path for the sample input:
Path: [(0,3) → (1,3) → (2,3) → (2,4) → (3,4) → (4,4) → (5,4) → (6,4) → (7,4)]
Cost: 107

## 🗺️ Path Visualization

Agent path marked with `★` | `S` = Start | `G` = Goal | `W` = Water | `F` = Flooded

```
Col:  0    1    2    3    4    5    6    7
    +----+----+----+----+----+----+----+----+
 0  |    |    |    | S  | W  | W  |    |    |
    +----+----+----+----+----+----+----+----+
 1  |    | F  | F  | ★  |    |    |    | F  |
    +----+----+----+----+----+----+----+----+
 2  |    |    |    | ★  | ★  |    |    |    |
    +----+----+----+----+----+----+----+----+
 3  | W  | W  |    | F  | ★  |    |    |    |
    +----+----+----+----+----+----+----+----+
 4  |    | F  |    |    | ★  |    | W  | W  |
    +----+----+----+----+----+----+----+----+
 5  |    |    |    | F  | ★  |    |    |    |
    +----+----+----+----+----+----+----+----+
 6  |    | W  | W  |    | ★  | F  |    |    |
    +----+----+----+----+----+----+----+----+
 7  |    |    |    |    | G  | F  |    |    |
    +----+----+----+----+----+----+----+----+

Path: (0,3)→(1,3)→(2,3)→(2,4)→(3,4)→(4,4)→(5,4)→(6,4)→(7,4)
Steps: 9  |  Cost: 107
```

### Complexity Comparison

| Metric               | Greedy Best-First | Genetic Algorithm |
|----------------------|:-----------------:|:-----------------:|
| Path Length          | 9 steps           | 9 steps           |
| Path Cost            | 107               | 107               |
| Fitness Score        | —                 | 3.67              |
| Nodes Expanded       | 10                | —                 |
| Nodes Generated      | 33                | —                 |
| Max Queue Length     | 11                | —                 |
| Population Size      | —                 | 50                |
| Generations Taken    | —                 | 26                |
| Execution Time       | ~0.00049s         | ~0.135s           |

> **Finding:** Greedy Best-First Search is significantly faster (~275×) than the 
> Genetic Algorithm. Both converge to the same optimal path, but the Genetic Algorithm 
> explores a wider search space, making it more robust for complex/larger grids.

---

## 🧠 PEAS Description

| Component | Description |
|-----------|-------------|
| **Performance** | Maximize safety score, minimize path length |
| **Environment** | 8×8 fully observable grid with empty, flooded, and water cells |
| **Actuators** | Move Up / Down / Left / Right |
| **Sensors** | Detect cell type — empty, water body, or flooded road |

---

## 🛠️ Setup & Usage

### Prerequisites
- Python 3.10+
- Jupyter Notebook or Google Colab

### Run Locally

```bash
git clone https://github.com/PriyankaMenghare/Grid-Navigation-Agent-Python.git
cd Grid-Navigation-Agent-AI-Search-Algorithms
jupyter notebook Grid_Navigation_Agent_AI_Search_Algorithms.ipynb
```

Run all cells in order. When prompted, enter the index number for your desired 
start and goal states.

---

## 📝 License

MIT License — for academic use.
