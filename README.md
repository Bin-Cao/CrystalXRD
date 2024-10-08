
# CrystalXRD project

An illustration that depicts the management of a crystal database.

## Crystal Database ([link](https://huggingface.co/datasets/caobin/CrystalXRD))

The `CryDB.db` is a crystal database that contains 723,158 pieces of crystals:
- 154,718 crystals from the MP dataset, March 8, 2024
- 55,723 crystals from the Jarvis dataset, March 8, 2024
- 512,717 crystals from the COD dataset, May 8, 2024

## demo.db

The `demo.db` shared here is a demo for illustrating the toolkit to manage the database.

## Toolkit (see code.ipynb)

### 1. Show and Query Data

To show and query each data entry, use the `CryDBkit` package:


```python
from CryDBkit import website

website.show('demo.db')
```

### 2. Graph Embedding of Each Data Entry

To perform graph embedding on each data entry, use the `Crylearn` package:

`Python==3.9.19`

```python
from Crylearn import cry2graph
from ase.db import connect

database = connect('demo.db')
entry_id = 1

node_embedding, _, dis_matrix, XRDpattern = cry2graph.parser(database, entry_id).get(model='Simulation')
```

Parse the crystal by lattice cell. Each atom contained in the lattice is a node with a 106-dimensional embedding (N * 106). The distance between any pair of nodes is given in the distance matrix (N * N). `XRDpattern` is the simulated diffraction pattern of the crystal.

- `node_embedding` (np.ndarray): The node embeddings, 106-dimensional.
- `distance_matrix` (np.ndarray): The distance matrix in Cartesian coordinates.
- `XRDpattern` (np.ndarray): Global information about the graph, 3501-dimensional.
