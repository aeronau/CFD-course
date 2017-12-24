# Simulation of a pipe

For an incompressible, stady-state with turbulence simulation, the simpleFOAM solver has to be used.

1. In `/opt/openfoam4/applications/` solvers and utilities are found. snappyHexMesh utility is in `/opt/openfoam4/applications/utilities/mesh/generation/snappyHexMesh`. `/opt/openfoam4/applications/utilities/mesh/generation/snappyHexMesh/snappyHexMeshDict` is the dictionary containing information for the utility.
2. Copy `snappyHexMeshDict` and `meshQualityDict` to the `/YPipe/system` folder of the simulation to be run. In this simulation, tutorial pitzDaily---found in `/opt/openfoam4/tutorials/incompressible/simpleFoam/pitzDaily`---is taken as reference. Files copied will be modified.
3. Create folder `/YPipe/constant/triSurface`. Add `pipe.stl` in this folder. This defines the geometry.
4. Run ` ` in `/YPipe/constant/triSurface/`. 
5. Run `surfaceCheck` to get information about the geometry.
6. Running `surfaceTransformPoints -scale '(0.01 0.01 0.01)' pipe.stl pipe.stl` will scale the `stl` geometry from m to cm. The geometry was created using Salome with o units defined.
7. In order to see the geometry ParaView can be used. The user has to run `paraview pipe.stl`.
8. Change vertices in `blockMeshDict` so the bounding box is the same as the bounding box of the geometry. See [Bounding box of the geometry](boundingBox.png). In this file change `convertToMeters` to 0.01 so the program understands that the dimensions are in cm, the same unit as the scaled file `pipe.stl`. The cells in which the box will be divided, have to be as square as possible. So in `blocks` it will be written `hex (0 1 2 3 4 5 6 7) (17 20 1) simpleGrading (1 1 1)`. The `boundary` section is now irrelevant.
9. Run `foamJob -s blockMesh` in the root folder of the simulation.
10. Run `paraFoam &` to visualize the mesh. In ParaView open the `pipe.stl` geometry file. If all the steps have been followed correctly, the object will appear placed as desired inside the mesh.
11. In file `snappyHexMeshDict`change stl name to `pipe.stl` and add regions `inlet1` with `name inlet1`, `inlet2` with `name inlet2`, `outlet` with `name outlet` and `pipe` with `name pipe`.
12. snappyHexMesh tool is good to mesh the surfaces but bad to mesh the edges. The user has to run another program that extracts information about the edges. The section `features` is used to pass edge information to the utility. In each region the user also has to define patchInfo---it says if there is flow going through the surface---. Add `type patch/wall;` and `inGroups (meshedPatches/walls)`
13. Change `locationInMesh` and add random decimal numbers to the desired value to avoid problems.
14. Copy `surfaceFeatureExtractDict` to the `system` folder and modify it accordingly.
15. Run `sufraceFeatureExtract` to obtain the eMesh file.
16. Run `foamJob -s snappyHexMesh` to finally mesh.
17. With paraview the user can see whether the mesh is correct or not.
18. Modify files `p` and `U` from folder `0.org` accordingly.
19. Create a backup of `0.org` named `0`.
20. In `constant/turbulenceProperties` add `simulationType laminar`.
21. Run `foamJob -s simpleFoam` to output the results of the simulation.
22. View results with `paraFoam`.
