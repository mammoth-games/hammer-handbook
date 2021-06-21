# Costume Specification

This specification codifies the creation and importing of a costume. It is underpinned by two constraints:

1. Reused meshes should use the originally imported mesh
2. Reuse textures whenever possible

These stem from the memory limitations of mobile hardware; the importance of reducing texture and mesh memory cannot be overstated.

## General Information
A costume is a set of textured meshes that are welded to the character. A costume is composed of 3 sections: Head, Torso, and Legs. Each section is further composed of meshes that are welded to specific body parts of the character.

| Costume section | Character body parts |
| --- | --- |
| Head | Head |
| Torso | LeftArm, RightArm, Torso |
| Legs | LeftLeg, RightLeg|

<img src="https://mammoth-games.github.io/hammer-handbook/img/character_sections.png" alt="character sections" width="512"/>

Players can mix and match the 3 sections of any costumes they own.

### Variations
Costumes may have multiple variations. Variations may use unique meshes and unique textures for body parts. Variations may also reuse meshes and textures for body parts. If a variation reuses a mesh, that mesh will not be re-uploaded.
!!! warning
	Because reused meshes are not re-uploaded, you are bound to the UV map of the original mesh. Keep this in mind when you are creating the variation's texture.

### Eyes
Costumes cannot have their own eye meshes, as an eye animation system will be used for facial expressions that react to the game. However, costumes can specify which eyes to hide and where they are located.

### Skin
Humanoid costumes (ex. pirate, chef, miner) have skin exposed. It is important that players be able to customize their skin color. To accomplish this, map the UV islands of skin faces to a transparent pixel. This will allow for the color of the underlying Roblox object to show through, which will be the player's skin color.
## Texturing

## Process
1. Modeler creates the costume
2. Modeler organizes the file to follow this specification
3. Modeler uploads the file to the drive
4. Programmer downloads the file
5. Programmer records the costume's metadata
6. Programmer imports the individual meshes of the costume
7. Programmer incorporates the metadata and meshes into the game

## Naming
1. Name the file `[costume]_[variation]_Costume.blend` *(ex: Pirate_Blackbeard_Costume.blend)*
2. Put the unaltered rig in a `Rig` collection. Hide or delete any of the limbs that you don’t need. *(ex: Pirate doesn’t need the left leg because it would cover the peg leg)*
	* These meshes will not be imported to Roblox but are helpful in previewing the costume in full context.
3. Put the costume meshes in a `[costume]_[variation]` collection. *(ex: Pirate_Blackbeard)*
4. For each of the 6 body parts:
	* If only one mesh corresponds to a body part, name it `[body part]` *(ex: LeftLeg)*
	* If multiple objects correspond to a body part, put them in a collection named `[body part]`. Name each object in this sub-collection
		`[body part]_[thing]`. *(ex: Head_Eyepatch)*
5. Name every vertex object the same as its mesh name.
	* Not sure if this is necessary. I will figure it out.
6. Set every object’s pivot to its corresponding body part’s pivot.
	* This is necessary. If you stick to the naming conventions, I can write a script to automate this step.
7. Put the Rig eyes in an `Eyes` collection in the `[costume]` collection. Position them as you please. Delete any unneeded eyes *(ex: Pirate doesn’t have a left eye due to the eye patch)*. If no eyes are needed, don’t create the `Eyes` collection.
## Metadata
For transparency between modelers and programmers, here is the metadata for each costume that will be stored in the game.

| Category | Variable | Value type | Required |
| --- | --- | --- | :---: |
| | CostumeName | `string` | ✓ |
| | VariationName | `string` | ✓ |
| Head | | |
| | HeadHidden | `boolean` |
| | HeadMeshId | `rbxassetid://` |
| | HeadTextureId | `rbxassetid://` |
| Legs | | |
| | LeftLegMeshId | `rbxassetid://` |
| | LeftLegTextureId | `rbxassetid://` |
| | RightLegMeshId | `rbxassetid://` |
| | RightLegTextureID | `rbxassetid://` |
| Torso | | |
| | LeftArmMeshId | `rbxassetid://` |
| | LeftArmTextureId | `rbxassetid://` |
| | RightArmMeshId | `rbxassetid://` |
| | RightArmTextureId | `rbxassetid://` |
| | TorsoMeshId | `rbxassetid://` |
| | TorsoTextureId | `rbxassetid://` |
| Eyes | | |
| | LeftEyePosition | `Vector2` |
| | LeftEyeHidden | `boolean` |
| | RightEyePosition | `Vector2` |
| | RightEyeHidden | `boolean` |

### Implementation details

* If "_MeshId" is not specified, then "_TextureId" will be ignored
* If "_MeshId" is not specified, then the body part will fall back to the default character mesh
* "_Hidden" will hide a body part altogether
* If "_Hidden" is specified, then "_MeshId" and "_TextureId" are ignored
* If "_EyeHidden" is specified, then "_EyePosition" is ignored
* If "_EyePosition" is not specified, then the eye falls back to the default position