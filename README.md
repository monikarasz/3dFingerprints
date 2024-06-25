# 3dFingerprints
Goal:
To represent molecules of various sizes as fixed-length vectors that allow for an accurate prediction of physical and chemical properties.

What happens in the code?
1) Preprocessing: creating a rotation-and-translation-independent representation of atom positions within a molecule (by introducing an internal coordinate system for each molecule)
2) Training of a regression model with an intermediate output (fixed-length vector):
   - input x: graph representations of molecules, consisting of node features (position (x,y,z) and atomic number of each atom) and adjacency matrix
   - input y: dipole moments of the molecules (real numbers)
   - output: predicted dipole moments
   - intermediate output: latent space representations of molecules (fixed-size vectors)
3) Training of regression models for various physical and chemical properties:
   - input x: vectors obtained from the first network
   - input y: real number (representing a physical/chemical property)
   - output: prediction
The dataset is shuffled between steps 2 and 3.

Requirements:
pytorch 2.3.0+cu121
pytorch geometric 2.5.3
numpy 1.25.2
scipy 1.11.4
matplotlib 3.7.1
pandas 2.0.3

The notebook works fine in google colab, although pytorch geometric requires a separate installation (first cell).
The dataset used (QM9, https://pytorch-geometric.readthedocs.io/en/latest/generated/torch_geometric.datasets.QM9.html ) is loaded directly from torch geometric.

Issues:
- molecules, for which the geometrical centre and the 2 atoms most distant from it are collinear were excluded from the data set
- the preprocessing might not lead to a unique position representation if the 2 atoms most distant from the geometrical centre of the molecule are equally distant from it


