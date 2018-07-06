---
layout: post
title:  "Animation Layer Bug in Maya"
date:   2018-07-05
comments: true
line_numbers: true
categories: maya python code animation
tags: [maya, python, code, animation]
---

So, been fighting this one for a while now. There's this nasty little bug in Maya 2017 (and I believe it exists in previous versions as well) where animation files that have a referenced rig AND animation layers will randomly save invalid connectAttr calls that cause animation layer nodes to connect to themselves (output connects to one if its own input attributes rather than the proper control). This creates cycles, Maya screams at us, and everyone is sad. Worse yet, this bug doesn't demonstrate itself until someone re-opens the file and the scene is reconstructed and the faulty connectAttr call reconnects the node to itself, removing the proper animCurve connection.

Fortunately, this seems to be a rare occurrence and everything is great. Unfortunately, this seems to be a rare occurrence and it bites us in the ass when an animator opens a file the next morning, we go to do a batch export, or someone re-visits an animation from days/weeks/months ago. Some times, it's a quick fix of reverting the the previous unbroken file and updating the animation again (small tweak in a layer). Other times, considerable work is lost, and losing work sucks. But alas, the work is not truly lost as all the animation curves are still retained in the scene. So I finally took some time this morning to properly work through and understand the problem and wrote some code to help alleviate the issue:

<div id="hf3dcode">
    <script src="https://gist.github.com/hoorayfor3d/516ff28a9a979183c9de35e3bb5bd719.js"></script>
</div>

Ultimately what's happening here is we're looking for animation layer nodes that connect to other animation layer nodes (themselves). We break those connections while tracking what inputs to reconnect. We then look for orphaned animCurve nodes that contain the name of the layer node and hook everything back up.

It's still and early pass, but in initial testing, it's corrected all the cycle warnings, got the animation back into the proper working state. It works with multiple layers regardless of their name. Seems like a useful snippet of code, so wanted to share it out for anyone else that might be encountering this fun little gem.
