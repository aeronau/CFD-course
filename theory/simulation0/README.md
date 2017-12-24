# Basic simulation

## openFOAM run

Here is a compilation of the steps followed in the first simulation.

1. In file `/home/arnau/Desktop/CFD-course/courseCases/icoFoam/cavity/cavity/constant/transportProperties`, values of the nu array [ 0 2 -1 ... ] are mass, length and time, respectively.
2. In file `/home/arnau/Desktop/CFD-course/simulation0/icoFoam/cavity/cavity/system/controlDict`, typical simulation parameters can be changed.
3. `*Dict` is the dictionary containing information for the `*` application. For example, `blockMeshDict` in `/home/arnau/Desktop/CFD-course/simulation0/icoFoam/cavity/cavity/system/` is the information file for the `blockMesh` application.
4. Go to `/home/arnau/Desktop/CFD-course/simulation0/icoFoam/cavity/cavity/` and run `blockMesh` command. The output of the run of `blockMesh`---aka the log---can be saved to a file by using `blockMesh > blockMesh.log`. Then, the information aforementioned will not appear.
5. In directory `/home/arnau/Desktop/CFD-course/simulation0/icoFoam/cavity/cavity/constant/polyMesh/` are the files that characterize the mesh. Filenames are self explanatory: `points` file is the collection of points that define the mesh.
6. `foamJob -s blockMesh` will execute `blockMesh` and produce a logfile as well as screen output.
7. `paraFoam` will call `paraview` with certain parameters initialized? so the results of the simulation are visualized quasi as soon as the application opens: the user only needs to press `Apply`.
8. Run `foamJob -s icoFoam` to run the simulation and store the results in a file while also getting screen feedback.
9. If the user doesn't know which word to put in a certain place of the file, writing `banana`---a word which makes no sense---the program will complain but provide a list of suitable words.
10. `icoFoam` doesn't solve for the pressure---measured in Pa---but for the pressure over the density---of units m squared over seconds squared.

## ParaView

- The pipeline browser is a graphical view of the flow of information across the tools. 

1. In order to visualize a vector field go to Sources > Search > Glyph. 
2. Stream Tracer allows the user to see the streamlines that pass through a point or a line---it can be selected in the Properties window.
