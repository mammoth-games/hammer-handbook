# Costume Specification

1. Name the file `[costume]Costume.blend` *(ex: PirateCostume.blend)*
2. Put the unaltered rig in a \texttt{Rig} collection. Hide or delete any of the limbs that you don’t need. *(ex: Pirate doesn’t need the left leg because it would cover the peg leg)*
3. Put the costume meshes in a \texttt{[costume]} collection. *(ex: Pirate)*
4. Every object should correspond to one of 6 body parts: Head, LeftArm, LeftLeg, RightArm, RightLeg, Torso.
	* If only one object corresponds to a body part, name it `[costume][body part]` *(ex: PirateLeftLeg)*
	* If multiple objects correspond to a body part, put them in a collection named `[costume][body part]`. Name each object in the sub-collection
		`[costume][body part][thing]`. *(ex: PirateHeadEyepatch)*
5. Name every mesh the same as its object name.
	* Not sure if this is necessary. I will figure it out.
6. Set every object’s pivot to its corresponding body part’s pivot.
	* This is necessary. If you stick to the naming conventions, I can write a script to automate this step.
7. Put the Rig eyes in an `Eyes` collection in the `[costume]` collection. Position them as you please. Delete any unneeded eyes *(ex: Pirate doesn’t have a left eye due to the eye patch)*. If no eyes are needed, don’t create the `Eyes` collection.