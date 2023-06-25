# Ligand Protected Nanocluster Database

Welcome to the Ligand Protected Nanocluster (LPNC) Database! This repository provides access to a comprehensive database of LPNCs. The information about each nanocluster, such as metal composition, ligands, properties like Ionization Potential (IP), Electron Affinity (EA), and file paths to their atomic structures, are organized neatly in an SQLite database for easy access.

## Database Structure

The main database file is `NC_Database.sqlite`. It contains a table named `NC_Data` with the following columns:

- `NC`: The name of the nanocluster
- `n_metal_1`, `n_metal_2`, `n_ligand`: The number of metal and ligand atoms
- `metal_1`, `metal_2`: The types of metal atoms
- `Dopant_Location`: The location of dopants, if any
- `ligands`: The type of ligands
- `q`: The base charge of the cluster
- `E_q_eV`, `E_q-1`, `E_q.1`: Energies at different charge states
- `EA`: Electron Affinity
- `IP`: Ionization Potential
- `HOMO`, `LUMO`: Energies of HOMO and LUMO
- `GAP`: Energy Gap
- `path`: Relative path to the atomic structure of the nanocluster
- `Reference Publications`: Reference publication link for the nanocluster

## Atomic Structures

The structure files are in .xyz format and the path to each of these files is updated in the main database.

## Using the Database

You can query the database using any SQLite client. If you prefer to use Python, you can use the `sqlite3` module. Here's an example of how you can load the data into a pandas DataFrame:

```python
import sqlite3
import pandas as pd

# Create a connection
conn = sqlite3.connect('NC_Database.sqlite')

# Query all records in the database
df = pd.read_sql_query('SELECT * FROM NC_Data', conn)

# Close the connection
conn.close()

# Now df is a pandas DataFrame containing all the data
```

If you want to work with the atomic structures, you can access them using the paths in the `path` column. For example, you can load an .xyz file using the Atomic Simulation Environment (ASE) package in Python as follows:

```python
from ase.io import read

# Load the atomic structure into an ASE Atoms object
atoms = read(df['path'][0])
```

## Contributing 

Contributions are always welcome! If you have any suggestions, bug reports, or just want to improve the database, please open an issue or submit a pull request.

## License

This project is licensed under the GPL-3.0 License. See the LICENSE file for details.

## Acknowledgements

We would like to acknowledge all the researchers and publications we have referred to while compiling this database.