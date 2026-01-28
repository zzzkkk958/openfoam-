# openfoam-hotroom-similation
用openfoam模拟空调向房间内部吹热风导致房间内部温度变化的仿真模拟

##模型说明
由数千平米的厂房空调房系统简化而来。大厂房中的空调入风口一般在天花板，出风口在入风口的上面。本模型采用这种思路。

##重要文件说明
.blender文件：blender制作的模型文件，读者可以导入到blender中查看模型的参数。
.stl文件：从blender导出的stl文件，方便使用snappyHexMesh雕刻。
0文件夹：内部存放物理场。

##项目使用说明
注：项目使用的openfoam版本是2506，paraview版本是5.13，Ubuntu版本是22.04，以下的命令都在Ubuntu终端中输入。
1.下载好我的项目后，用VsCode打开文件夹。（也可以用记事本打开，但是VsCode比较方便）
2.输入命令：blockMesh
3.输入命令：checkMesh。得到Mesh OK。
4.输入命令：surfaceFeatureExtract
5.输入命令：snappyHexMesh -overwrite
6.输入命令：buoyantBoussinesqPimpleFoam.开始进行计算，这一过程要几分钟。
7.输入命令：touch hotroom.case.会生成一个名为hotroom.case的文件.
8.打开paraview，打开hotroom.case.即可查看示例。

##自主创建项目的方法
1.blender建模出你想要的模型。
2.把模型导出为stl文件。
注意：openfoam中Y轴向上，Z轴向前；blender中Z轴向上，Y轴向前，导出文件时要反转一下。
注意：如果你的模型有不同的部分，比如我的模型中有空调入风口（inlet），空调出风口（outlet），墙壁（wall），那就每个部分导出为一个stl文件。
注意：如果你有两个入风口，如果吹风方向和速度一致，可一起导出，如果方向和速度不一致，就分别导出为inlet1和inlet2...
注意：0文件夹下物理场内部的boundry内部的名称必须与.stl文件的名称完全一致。
注意：如果你的stl文件与我的不一样，需要在system文件夹下的snappyHexMeshDict内部的geometry、features、refinementSurfaces和surfaceFeatureExtractDict内容同步修改。
3.stl文件存放在constant文件夹下的triSurface文件夹内部
4.在blockMeshDict中创建一个能包住你的blender模型的立方体。
5.执行上述“项目使用说明”中的命令
