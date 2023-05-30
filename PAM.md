Viewing a PAM requires 3 main components - 
1) The RESOURCES.rton file (path: "PROPERTIES/RESOURCES.RTON")
2) The PAM file (path: "IMAGES/768/INITIAL/[category]/[name].PAM")
3) The PTX file (path: "ATLASES/[name].PTX")

# RESOURCES.RTON  
<b>Structure:</b>
<b>
- version - <i>Integer. Usually 1. Purpose not known/not that useful.</i>
- content_version - <i>Integer. Usually 1. Purpose not known/not that useful.</i>
- slot_count - <i>Integer. Purpose not known/not that useful.</i>
- groups[]
  - type - <i>String. Possible values: "simple", "composite". If "composite", it means that the group is made up of several subgroups. If "simple", the group contains the data of a specific component such as the atlas, the animation or the soundbank.</i>
  - id - <i>String. Name of the group.</i>
  - subgroups[] - Array of subgroups under the group. Only present if group is of type "Composite".
    - id - <i>String. Name of the subgroup.</i>
    - res - <i>Integer. Resolution of the atlas under the subgroup. Only present if subgroup is an atlas.</i>
  - res - <i>Integer. Resolution of the atlas contained in the group. Only present if group is an atlas.</i>
  - parent - <i>String. The parent group that this group is a part of. Only present if this group is a subgroup.</i>
  - resources[] - <i>Array of resources (atlases, parts of atlases, animations, soundbanks, etc.) under the group. Only present if group is of type "Simple".</i>
    - type - <i>String. Possible values: "Image", "PopAnim", "SoundBank". If "Image", it means that the resource is an atlas or a part of an atlas. If "PopAnim", the resource is an animation. If "SoundBank", the resource is of course a soundbank.</i>
    - slot - <i>Integer. Purpose not known/not that useful.</i>
    - id - <i>String. Name of the resource.</i>
    - path - <i>String. The path at which the resource is present or where it is generated.</i>
    - atlas - <i>Boolean. If true, it means that the resource is an atlas. Only present if resource is of type "Image" and an atlas texture.</i>
    - runtime - <i>Boolean. Usually true. Purpose not known/not that useful. Only present if resource is of type "Image" and an atlas texture.</i>
    - width - <i>Integer. Width (in pixels) of the atlas texture referenced by the resource. Only present if resource is of type "Image" and an atlas texture.</i>
    - height - <i>Integer. Height (in pixels) of the atlas texture referenced by the resource. Only present if resource is of type "Image" and an atlas texture.</i>
    - parent - <i>String. Parent atlas of the atlas sub-texture contained in the resource. Only present if resource is of type "Image" and an atlas sub-texture.</i>
    - ax - <i>Integer. The x index of the pixel in the atlas texture from which the sub-texture is drawn. Sub-texture is drawn from left to right. Only present if resource is of type "Image" and an atlas sub-texture.</i>
    - ay - <i>Integer. The y index of the pixel in the atlas texture from which the sub-texture is drawn. Sub-texture is drawn from top to bottom. Only present if resource is of type "Image" and an atlas sub-texture.</i>
    - aw - <i>Integer. The width of the sub-texture (in pixels). Only present if resource is of type "Image" and an atlas sub-texture.</i>
    - ah - <i>Integer. The height of the sub-texture (in pixels). Only present if resource is of type "Image" and an atlas sub-texture.</i>
    - forceOriginalVectorSymbolSize - <i>Boolean. Usually true. Purpose not known/not that useful. Only present if resource is of type "PopAnim".</i>
</b>

# [name].PAM (e.g., ELECTRIC_PEASHOOTER.PAM)
<b>Structure:</b>
<b>
- frame_rate - <i>Integer. Usually 30. Framerate of the animation in fps.</i>
- position - <i>Array of 2 Floats. Usually [0.0, 0.0]. Probably contains the x and y values to define the offset of the entire sprite.</i>
- size - <i>Array of 2 Floats. Contains the x and y values to define the size of the entire sprite, probably for the hitbox.</i>
- image[] - <i>Array of images to be loaded.</i>
  - name - <i>String. Name of the image. Contains the path name followed by the id name separated by '|' symbol (e.g., "electric_peashooter_67x61|IMAGE_PLANT_ELECTRIC_PEASHOOTER_ELECTRIC_PEASHOOTER_67X61").</i>
  - size - <i>Array of 2 Floats. Contains the size of the image (not in pixels, but w:h ratio must be maintained).</i>
  - transform - <i>Array of 6 Floats. Contains the affine transformation matrix in the order: a, b, c, d, tx, ty. Initial transform applied on the texture, usually only an offset.</i>
- sprite[] - <i>Array of sub-sprites to be loaded. Sub-sprite has same structure as main_sprite except for a few differences.
  1) It has only 1 frame.
  2) Value of name variable not an empty string.
  3) Value of work_area variable is usually [0, 0].
  </i>
- main_sprite - <i>Contains the main data for the animation of the sprite.</i>
  - name - <i>String. Name of the sprite. Usually an empty string.</i>
  - frame_rate - <i>Integer. Usually 30. Framerate of the animation in fps. Purpose unknown since global framerate is already specified.</i>
  - work_area - <i>Array of 2 Integers. Purpose not known/not that useful.</i>
  - frame[] - <i>Array of frames present in the animation of the sprite.</i>
    - label - <i>String. Name of the frame. If this frame is the starting frame for a particular sub-animation (idle, attack, etc.), it carries the name of that animation.</i>
    - stop - <i>Boolean. Specifies if the frame is a stop frame or not. A stop frame is the end of a particular sub-animation (idle, attack, etc.), after which the animation may loop or stop completely.</i>
    - command - <i>Array of commands. Each command is an array of 2 Strings: the name of the command (e.g., "PlaySample"), the command parameter (e.g., the sound file to be played, for instance, "Play_Plant_ElectricPeashooter_Idle_01").</i>
    - remove - <i>Array of elements to be removed from the screen.</i>
      - index - <i>Integer. Index of the element to be removed.</i>
    - append - <i>Array of elements to be added to the screen.</i>
      - index - <i>Integer. Index of the element to be added.</i>
      - name - <i>String. Name of the element to be added.</i>
      - resource - <i>Integer. Index of the resource to be used.</i>
      - sprite - <i>Boolean. If true, the resource index will reference the sprites indexed in the order in which they are present in sprite[]. If false, the resource index will reference the images indexed in the order in which they are present in image[].
      - additive - <i>Boolean. Purpose not known/not that useful.</i>
      - preload_frame - <i>Integer. Purpose not known/not that useful.</i>
      - time_scale - <i>Float. Purpose not known/not that useful.</i>
    - change - <i>Array of elements to be transformed with the necessary parameters.</i>
      - index - <i>Integer. Index of the element to be transformed.</i>
      - transform - <i>There are three possible values for this variable.
        1) Array of 6 Floats: Contains the affine transformation matrix in the order: a, b, c, d, tx, ty.
        2) Array of 3 Floats: Contains the affine transformation matrix in the order: rotation (in radians), tx, ty.
        2) Array of 2 Floats: Contains the affine transformation matrix in the order: tx, ty.
        </i>
      - color - <i>Array of 4 Floats. Contains the color for the sprite tint in the order: r, g, b, a.</i>
      - sprite_frame_number - <i>Purpose not known/not that useful.</i>
      - source_rectangle - <i>Purpose not known/not that useful.</i>
</b>
