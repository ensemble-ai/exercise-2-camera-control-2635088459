
# Peer-Review for Programming Exercise 2 #

## Description ##

For this assignment, you will be giving feedback on the completeness of assignment two: Obscura. To do so, we will give you a rubric to provide feedback. Please give positive criticism and suggestions on how to fix segments of code.

You only need to review code modified or created by the student you are reviewing. You do not have to check the code and project files that the instructor gave out.

Abusive or hateful language or comments will not be tolerated and will result in a grade penalty or be considered a breach of the UC Davis Code of Academic Conduct.

If there are any questions at any point, please email the TA.   

## Due Date and Submission Information
See the official course schedule for due date.

A successful submission should consist of a copy of this markdown document template that is modified with your peer review. This review document should be placed into the base folder of the repo you are reviewing in the master branch. The file name should be the same as in the template: `CodeReview-Exercise2.md`. You must also include your name and email address in the `Peer-reviewer Information` section below.

If you are in a rare situation where two peer-reviewers are on a single repository, append your UC Davis user name before the extension of your review file. An example: `CodeReview-Exercise2-username.md`. Both reviewers should submit their reviews in the master branch.  

# Solution Assessment #

## Peer-reviewer Information

* *name:* Jack Schonherr
* *email:* jmschonherr@ucdavis.edu

### Description ###

For assessing the solution, you will be choosing ONE choice from: unsatisfactory, satisfactory, good, great, or perfect.

The break down of each of these labels for the solution assessment.

#### Perfect #### 
    Can't find any flaws with the prompt. Perfectly satisfied all stage objectives.

#### Great ####
    Minor flaws in one or two objectives. 

#### Good #####
    Major flaw and some minor flaws.

#### Satisfactory ####
    Couple of major flaws. Heading towards solution, however did not fully realize solution.

#### Unsatisfactory ####
    Partial work, not converging to a solution. Pervasive Major flaws. Objective largely unmet.


___

## Solution Assessment ##

* Note: In every camera, the programmer set `draw_camera_logic` to `true` in the `_ready()` function, but none of the cameras actually show their lines until the user manually turns them on. I omitted this error from each individual stage's review and instead decided to focus on the actual camera implemenations, though each stage is technically incomplete when considering the `draw_camera_logic` error.

### Stage 1 ###

- [x] Perfect
- [ ] Great
- [ ] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

___
#### Justification ##### 
The camera is properly centered on the vessel and follows its location precisely, shown by the cross draw in the center of the screen. It also follows the vessel when it's moving at hyperspeed.

___
### Stage 2 ###

- [x] Perfect
- [ ] Great
- [ ] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

___
#### Justification ##### 
The pushbox scrolls at a constant speed and is properly defined by a drawn bounding box. The vessel cannot move outside of the box and when it is touching the borders, it is stuck moving at the autoscroll speed. The vessel also gets pushed around by the box when touching the back wall. It behaves correctly when changing the `autoscroll_speed` to new values. Everything still works when the vessel is moving at hyperspeed, too.

___
### Stage 3 ###

- [ ] Perfect
- [x] Great
- [ ] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

___
#### Justification ##### 
The camera smooths out the position locking pretty well. When moving in a given direction, the cross drawn in the center of the screen lags behind the the vessel in that direction.  Once the `leash_distance` is reached, the camera remains a constant distance away from the vessel. Swithcing directions is smooth and responsive. However, there are some bugs when changing parameters. `catchup_speed` is set to `10.0` by default, and this seems relatively smooth. However, when I change this value to `2.0`, the camera is able to drift significantly further behind the vessel. I did not change `leash_distance` at all, but it the gameplay would suggest that I did. When I changed the `catchup_speed` to `20.0`, it made the camera extremely jittery when at `leash_distance` away from the vessel.

___
### Stage 4 ###

- [ ] Perfect
- [ ] Great
- [x] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

___
#### Justification ##### 
The camera correctly "looks ahead" of the vessel's position by smoothly moving to a position in front of it in the direction it is moving, shown by the cross drawn in the middle of the screen. Switching directions while looking ahead is smooth and responsive. However, the implementation is completely missing the required exported variable `catchup_delay_duration`. There is no ability to add a delay before the camera catches up to the target; it is instant every time. There are also some bugs with changing the exported fields. `lead_speed` is set to `18.0` by default. Raising this value doesn't seem to have issues, but lowering seems to have the unintended consequence of messing with the leash distance. As I keep lowering `lead_speed` (while not touching `leash_distance`), the camera is able to look ahead less and less and eventually turns into a stage-three-like camera that drifts behind the vessel.

___
### Stage 5 ###

- [ ] Perfect
- [ ] Great
- [ ] Good
- [x] Satisfactory
- [ ] Unsatisfactory

___
#### Justification ##### 
The two zones are properly drawn. When the vessel is in the middle zone, the camera does not move. When the vessel is in the speedup zone, it moves at `push_ratio` * the vessel's speed. However, when the vessel reaches the edge of the outer box, the camera doesn't appear to move at the vessel's base speed. Instead, it continues to move slowly. For some reason, the vessel's speed is being altered in the camera. The camera controller should be the only thing moving in this script. When the vessel is touching the edge of the pushbox, its speed is slowed down, preventing it from moving at its base speed like it should be able to. In addition, there is a `const EDGE_BUFFER` that is documented as existing to prevent stuttering when the vessel is at the edge of the pushbox. This creates imperfect boundaries where the vessel sticks out past the push box edge, so the push box defined by the user is not its true size. There is also some weird inner buffer that pushes the push box edge away from the vessel after letting go of a direction input. Lastly, the camera moves when the vessel is moving towards the center region, and this should not happen. Movement should only occur when moving away from the center.
___
# Code Style #


### Description ###
Check the scripts to see if the student code adheres to the dotnet style guide.

If sections do not adhere to the style guide, please peramlink the line of code from Github and justify why the line of code has not followed the style guide.

It should look something like this:

* [description of infraction](https://github.com/dr-jam/ECS189L) - this is the justification.

Please refer to the first code review template on how to do a permalink.

#### Style Guide Infractions ####

One minor infraction I found was the placement of a `const` variable in a class. According to the style guide, they should be placed before `@export` variables, but [in this example](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/speedup_push_zone.gd#L17), there is a `const` after the `@export` variables. This is is pretty minor in my opinion.

#### Style Guide Exemplars ####

The programmer obviously took lots of care to adhere to the study guide. Every script they wrote is incredibly well organized. They follow the guideline of spacing out logical chunks of code to a T, and one example of this is [here](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/speedup_push_zone.gd#L65). They sectioned off groupings of local variables in a way that is very easy to follow.

They also formatted a multiline boolean [here](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/speedup_push_zone.gd#L58). This was much easier to read than having all of this same information in a single line. 
___


#### Put style guide infractures ####

___

# Best Practices #

### Description ###

If the student has followed best practices (Unity coding conventions from the StyleGuides document) then feel free to point at these code segments as examplars. 

If the student has breached the best practices and has done something that should be noted, please add the infraction.


This should be similar to the Code Style justification.

#### Best Practices Infractions ####

The programmer did not statically type any of their local variables. For some variables, this is not a huge deal because the type can be inferred by a reader (e.g. a variable called position is easily inferred as a Vector3). For others, it is much more detrimental. In the [multiline boolean example](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/speedup_push_zone.gd#L58) I referenced earlier as an exemplar of the style guide, the type is not statically defined. At first glance, someone reading this code would have no idea what the type is. The comment also doesn't tell the reader anything about the type, so they have to do some more digging. Adding static types is better practice.

Looking at the Github repo, I noticed there are only two commits. One is for every piece of code they wrote, and the other is for a `README.md` update. It is much better practice to be making consistent commits once small features are implemented. It is also good practice to work in branches instead of committing straight to the master branch, but for a tiny, isolated project like this it's not as big of a deal. I also noticed the commit message for the first commit is "updated e2". I don't know what this means, and it is good practice to make concise but descriptive commit messages so that you and others can look back and understand what an individual commit changes.

#### Best Practices Exemplars ####

There are comments EVERYWHERE. Sometimes it feels like there are too many (there are some trivial things like [setting positions](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/position_lock_camera.gd#L22) which don't need to be explained), but in general I think it is great to have so many comments. They are incredibly descriptive and make understanding the code much easier. One of the best example of this is [here](https://github.com/ensemble-ai/exercise-2-camera-control-2635088459/blob/126f5e360a233f2346c4059771aa0790c4b0c27e/Obscura/scripts/camera_controllers/position_lock_and_lerp.gd#L40) explaining the boolean to float conversion taking place. It is not easy to understand what this code does at first glance, so the comment is very useful.
