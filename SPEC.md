# Parallel Parking Simulator

## Game idea

A single-player, top-down parking game where you use the arrow keys to parallel park a car between two parked cars. Successfully parking completes the level. There are three levels, and the space between the parked cars gets smaller each time.

The game should feel simple to understand but require careful steering and small adjustments. The challenge comes from maneuvering into a tight space without hitting anything.

## View and layout

- Use a fixed top-down view showing the road, a curb on the right, two parked cars, and the player's car.
- The parked cars face toward the top of the screen and sit along the curb.
- Show a rectangular parking zone between the two parked cars.
- Make the player's car a different color and clearly show which end is the front.
- Start the player on the road beside the upper parked car, facing the same direction, with enough room to begin reversing into the space.
- Simple shapes are sufficient; detailed artwork is not required.

## Controls and movement

- Up arrow: drive forward in the direction the car faces.
- Down arrow: reverse.
- Left/right arrows: steer the front wheels left/right relative to the car.
- Steering changes the car's direction only while moving. The car cannot rotate in place or slide sideways.
- Reversing with the same steering input turns the car's heading in the opposite direction from driving forward.
- Releasing up/down stops the car. If both are held, the car stops. If both steering keys are held, steering is neutral.
- R: restart the current level.
- Enter: advance after completing a level; after the final win, restart from level 1.

Use slow, controllable movement. Detailed acceleration, gears, and realistic tire physics are outside the scope.

## Levels

All levels use the same car size and handling. Difficulty changes through the empty bumper-to-bumper distance between the parked cars.

| Level | Difficulty | Gap |
| --- | --- | --- |
| 1 | Easy | 2.0 times the player's car length |
| 2 | Medium | 1.6 times the player's car length |
| 3 | Hard | 1.3 times the player's car length |

The parking zone extends across this gap and is 1.4 times the player's car width, measured outward from the curb. Keep enough open road available to maneuver in every level.

These gap sizes are initial tuning values. If playtesting shows a level is impossible with the implemented steering, adjust the gaps and document the final values. Each successive level must still have a smaller gap, and all three must be completable.

## Success, collisions, and retries

A level is complete when all of the following remain true for one continuous second:

- The entire player car is inside the parking zone.
- The car faces within 10 degrees of the parked cars' direction.
- The car is stopped.
- The car is not touching either parked car or the curb.

After success, freeze movement and show "Parked! Press Enter for the next level." After level 3, show "You win! Press Enter to play again."

Touching a parked car, the curb, or the edge of the playable road ends the attempt. Freeze movement and show "Collision! Press R to retry." Collision takes priority over success.

Retries are unlimited and restart only the current level. There is no timer or score.

## Acceptance criteria

1. The game opens at level 1 in a top-down view with a player car, two parked cars, a curb, and a visible parking zone.
2. The player's front is visually identifiable, and its color differs from the parked cars.
3. Up and down move the car forward and backward relative to its current heading.
4. Left and right steer while moving, with opposite heading changes when reversing. Steering alone does not rotate the car.
5. Releasing the movement keys stops the car, and opposing inputs behave as described above.
6. Contact with either parked car, the curb, or a playable-road boundary freezes the attempt and displays the collision message. Collision checks account for the car's rotation.
7. Pressing R restores the current level's starting position and clears any collision, success, or parking-hold state.
8. A level completes only after the entire car is inside the zone, correctly aligned, stopped, and collision-free for one continuous second.
9. A car that is partly outside the zone, incorrectly aligned, moving, or touching an obstacle does not complete the level.
10. Success freezes movement and displays a clear completion message. Enter advances exactly one level.
11. There are exactly three levels, each with a smaller parking gap than the previous one. Car size and handling remain unchanged.
12. Each level can be completed through normal driving without passing through obstacles.
13. Completing level 3 displays the final win message. Enter then resets the game to level 1.
14. The current level and a short controls reminder remain visible during play.

## Priorities

- Highest priority: controllable forward/reverse driving, steering, collision detection, and reliable parking detection.
- Next priority: all three playable levels, progression, retry, and final win behavior.
- Lowest priority: visual polish beyond the simple shapes and labels needed to understand the game.

If time runs short, sacrifice decorative graphics and animations first. Prioritize a working first level before adding the remaining levels, and document any unmet criteria honestly.

## Scope

The full intended game is the three-level experience described above. Multiplayer, moving traffic, sound, leaderboards, realistic vehicle physics, and additional levels are not required.
