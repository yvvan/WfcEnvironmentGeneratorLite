Procedural Environment Generator Lite is based on WaveFunctionCollapse algorithm and allows to generate environments of the user-specified dimensions built from the prepared modules with connection rules.
This is a free version of https://www.unrealengine.com/marketplace/en-US/product/procedural-environment-generator-wfc

In the plugin description you can see the screenshots made after putting WfcActorLiteWithBlueprint (Content/Demo) into the scene and pressing button "Generate in Editor" in the WfcActorWithBlueprint details panel.
For the demo content it's not recommended to change "Ground", "Floor Border", "Air Border" and "Voxel Size" values.

The difference from the full version:
 - dimensions are limited
 - not possible to set the saved seed
 - not possible to generate environment at any point of the game
 - no network replication supported
Everything else works the same.

How to use this Plugin
-------------

Check out the video tutorial about the basics: https://www.youtube.com/watch?v=0t3A4YZM6ks

Demo
-------------
First check out the demo Blueprint where everything is already set up.
You have to enable "Show Engine Content" for the content browser and open WfcEnvironmentGenerator Content -> Demo -> WfcActorLiteWithBlueprint

With the example Blueprint you can generate the level right away.
To do that just press the button "Generate in Editor"!

Inside this Blueprint you can find:
1. "Generator" properties of WfcActorLite:
   - "X", "Y", "Z" are the dimensions of the generated level.
   - "Ground" is set to the name of WfcVoxelLite which will be used for the whole 0 floor. Empty field means no restrictions.
     In the example it's set to "solid".
   - "Floor Border" - restriction for the 1 floor edges (only for 1 voxel from the border). Empty field means no restrictions.
     In the example it's set to "floor".
   - "Air Border" - restriction for all floors except 0 and 1 (only for 1 voxel from the border) and for the whole top floor.
     Empty field means no restrictions. In the example it's set to "empty".
   - "Voxel Size" is the size of your mesh side. It is set to 200 which is the size of the mesh used in example.
   - "Last Seed" shows you the seed used to generate the last level. Save it and use in "Seed" field to recreate you level.
   - "Seed" field should be empty most of the time unless you want to recreate the level you generated earlier.
   - "Shadow Material" is used to replace the Element 0 material. It is used only to show the connected meshes (hints) in Blueprint.
     Don't set it if you don't want to see connected meshes.
   - "Generate in Play Mode" - select it to see interactive level generation after you press the Play button
2. WfcActorLite contains a set of voxels (based on UStaticMeshComponent class), each of them has additional properties split in 2 groups:
 2a. "WfcVoxelLite" properties:
   - "Weight" helps to adjust the frequiency of the mesh in level, has to be >= 1.
   - "X/Y/Z Plus/Minus Direction" is the number of connector used at this direction.
   - "X/Y Plus/Minus Direction Symmetry" has 3 values:
     - "Connects to Itself" means that this connector is symmetric.
     - "Straight" connects only with "Flipped" with the same number and vice versa.
   - "Z Plus/Minus Direction Symmetry" has 5 values:
     - "Any Rotation" is self explanatory.
     - "Rotate <T> Times" means that this voxel connects in this direction only when it's rotated T times.
       For example when first WfcVoxelLite has "Z Plus Symmetry" = "Rotate One Time" and second - "Z Minus Symmetry" = "Rotate Three Times"
       that means that the first one has to be rotated twice to match be connected to the second one.
 2b. "WfcVoxelLite Restrictions" properties:
   - "X/Y/Z Plus/Minus Excluded" - names of other voxels (neighbors) that you don't want to be connected to this one in this direction,
     even if their connectors match.

You may play with these properties to see how they effect the result of the generator.

Setting up your new Blueprint
-------------

1. Place "WfcActorLite" to your level
2. Press "Blueprint/Add Script", select the name.
3. Open Blueprint editor. Change the settings (see 4-8).
   For the settings description check the "Demo" section of this Readme.
4. Set "Shadow Material" for the root object (if you want to see the shadows). You may use "shadow" material from the "Demo" content.
5. Set dimensions and other settings of WfcActorLite in "Generator" properties tab.
6. Add "WfcVoxelLite" components to the DefaultSceneRoot.
7. Set up weights, connectors and excluded neighbors.
8. Do not set any mesh to the WfcVoxelLite if you want it to be empty (air for example).
9. In Unreal Editor (NOT in Blueprint editor) press "Generate in Editor" to generate your level.
10. The set of new actors will be spawned each containing the mesh you've set up earlier.
11. You can clean them with button "Clean Generated". Or save "Last Seed" if you want to generate the same level later.
12. To generate the same level again - paste your saved seed into "Seed" property and press "Generate in Editor".
13. If you want to see interactive generation you have to set "Generate in Play Mode" and press play button.

Content
-------------

Number of Blueprints: 1
Number of C++ Classes: 2 UCLASS, 2 UENUM, 16 plain C++ classes/structs
Network Replicated: No

Contact
-------------
If you have any Questions, Comments, Bug reports or feature requests for this plugin, or you wish to contact me you can and should email me - yv.ivan@gmail.com
