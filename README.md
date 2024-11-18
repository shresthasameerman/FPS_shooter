# PlayerController3D Script Documentation

## Overview

This script provides 3D character movement, jumping, mouse-controlled camera rotation, and a toggleable crouch mechanic with animations for a **Godot Engine** project. 

---

## Features

1. **Basic Movement**:
   - Smooth movement controlled via input actions.
   - Jumping with gravity simulation.

2. **Mouse-Controlled Camera**:
   - Rotate the camera using mouse movement.
   - Tilt limited to prevent disorienting rotations.

3. **Crouching Mechanic**:
   - Toggle crouch with smooth animations.
   - Prevent uncrouching when blocked (using a `ShapeCast` node).

4. **Customizable Settings**:
   - Easily adjust movement speed, camera sensitivity, and crouch speed.

---

## Node Requirements

Ensure the following structure and node assignments in your scene:

### Scene Tree
1. **CharacterBody3D**: Attach this script to the root `CharacterBody3D` node.
2. **Camera3D**: Assign the `CAMERA_CONTROLLER` property to this node.
3. **AnimationPlayer**: Assign the `animation_player` property and ensure it contains a `"crouch"` animation.
4. **ShapeCast**: Attach as a child node to the character and assign it to the `CROUCH_SHAPECAST` property.

---

## Properties

### Exposed Properties
| Property               | Type            | Description                                                                                          |
|------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `SPEED`                | `float`         | Movement speed of the character. Default: `10.0`.                                                   |
| `JUMP_VELOCITY`        | `float`         | Jump velocity. Default: `5.0`.                                                                      |
| `MOUSE_SENSITIVITY`    | `float`         | Sensitivity for mouse camera movement. Default: `0.5`.                                              |
| `TILT_LOWER_LIMIT`     | `float` (radians)| Minimum tilt angle for the camera. Default: `-90 degrees`.                                          |
| `TILT_UPPER_LIMIT`     | `float` (radians)| Maximum tilt angle for the camera. Default: `90 degrees`.                                           |
| `CAMERA_CONTROLLER`    | `Camera3D`      | Reference to the camera node for first-person movement.                                              |
| `animation_player`     | `AnimationPlayer`| Reference for handling crouch animations.                                                           |
| `CROUCH_SPEED`         | `float`         | Speed of crouch animation. Range: `5.0` to `10.0`. Default: `7.0`.                                   |
| `CROUCH_SHAPECAST`     | `Node`          | Reference to the `ShapeCast` node for collision detection while crouching.                           |

---

## Input Actions

Define these actions in **Project Settings > Input Map**:

| Action          | Suggested Key |
|------------------|---------------|
| `move_left`      | `A`           |
| `move_right`     | `D`           |
| `move_forward`   | `W`           |
| `move_backward`  | `S`           |
| `Jump`           | `Spacebar`    |
| `crouch`         | `Ctrl` or `C` |
| `exit`           | `Esc`         |

---

## Methods

### `toggle_crouch()`
Toggles the crouch state with animations.
- Prevents uncrouching if `CROUCH_SHAPECAST` detects a collision.

### `_update_camera(delta: float)`
Handles camera rotation based on mouse input, clamping tilt angles within the limits.

### `_physics_process(delta: float)`
Manages movement, jumping, and gravity in each physics frame.

---

## Usage Instructions

1. **Attach the Script**:
   - Add this script to your `CharacterBody3D` node.

2. **Set Node References**:
   - Assign the `CAMERA_CONTROLLER`, `animation_player`, and `CROUCH_SHAPECAST` properties in the inspector.

3. **Test Movement**:
   - Verify that movement, jumping, and camera rotation work as expected.

4. **Crouch Animations**:
   - Ensure the `AnimationPlayer` node has a `"crouch"` animation defined.

5. **Collision Detection**:
   - Position the `ShapeCast` node appropriately to detect obstacles above the character.

---

## Notes

- Adjust `CROUCH_SPEED` for faster or slower crouch animations.
- Ensure the camera's rotation clamps prevent disorienting movements.
- Extend the script to include additional mechanics like sprinting or climbing if needed.

---

## Troubleshooting

1. **Camera Rotation Issues**:
   - Check if `CAMERA_CONTROLLER` is assigned to a valid `Camera3D` node.

2. **Crouch Not Working**:
   - Ensure the `"crouch"` animation exists in the `AnimationPlayer`.
   - Verify the `ShapeCast` node is positioned correctly.

3. **Jump Not Responding**:
   - Confirm the `Jump` input action is mapped correctly.

---

This script offers a customizable, modular character controller for your 3D game projects in Godot. Enjoy coding! 🎮
