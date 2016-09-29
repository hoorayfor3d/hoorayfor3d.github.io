---
layout: post
title:  "Accessing State Weights From Code"
date:   2016-09-28
comments: true
line_numbers: true
categories: ue4 cpp code animation
tags: [ue4, cpp, code, animation]
---

Recently, I've be doing a lot of work to optimize animation blueprints in UE4 by moving all of the
event graph functionality into C++. One particular problem I ran into was that I was unable to
['Fast Path Enable'] several blend nodes due to their alpha values being driven by state weights
from various state machines within the graph.

I quickly found out that you can easily get the weight of any state from the graph in code, but you
needed to know the index of both your state machine and your animation state. The animation instance
didn't offer any method of getting a state index from just a name, but the [FBakedAnimationStateMachine]
struct does have a [FindStateIndex()] function that does just that. Below is an example of a simple
function that I added to my custom AnimInstance that returns a state's index based on the name of
the state.

<div id="hf3dcode">
    <script src="https://gist.github.com/hoorayfor3d/6bc09f1113f32cdae4eda551fdf73f06.js"></script>
</div>

To get the index of a given state machine, you can use [GetStateMachineIndex()] within your
AnimInstance. That can then be passed in to the above function with the name of your state to
retrieve the index. From there, it's a matter of calling [GetInstanceStateWeight()] with the index
of both the state machine and your animation state to get the current blend weight of your state.

['Fast Path Enable']: https://docs.unrealengine.com/latest/INT/Engine/Animation/Optimization/FastPath/
[FBakedAnimationStateMachine]: https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Animation/FBakedAnimationStateMachine/index.html
[FindStateIndex()]: https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Animation/FBakedAnimationStateMachine/FindStateIndex/index.html
[GetStateMachineIndex()]: https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Animation/UAnimInstance/GetStateMachineIndex/index.html
[GetInstanceStateWeight()]: https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Animation/UAnimInstance/GetInstanceStateWeight/index.html
