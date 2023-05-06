# Assembly from a Multi-Body Part
\label{cha:building-hinge-assembly}

One of the miracles of modern mechanical design is that all of the pieces fit together so damned well. This fact is largely thanks to advances in CAD and digital part visualization. Compare the engine compartments of cars in Figure~\ref{fig:engine-compartments}

![\label{fig:engine-compartments}](images/figures/engine-compartments.png)

Though not all of this development is for the better (see Box~\ref{aside:ups-and-downs-of-cad}), it has enabled new products. The smartphone wouldn't fit in your pocket if it were developed with the methods of 1950. 

In this chapter, we'll begin to leverage this magic. Our goal is to design a door assembly (Figure~\ref{fig:door-assembly-completed}). Unlike the bracket from Chapter~\ref{cha:tee-connector} and \ref{cha:tee-bracket-assembly}, our door assembly will have two custom parts, the door and the frame, rather than one. If we develop the model well, these components will change together and preserve design intent. Both the door and the frame will be robust to changes in dimension as well as hinge choice.

![\label{fig:door-assembly-completed}](images/figures/door-assembly-completed.png)

Speaking of design intent:

\questiontriangle What is the design intent of this system? In other words, if we develop a frame-door-hinge-ground system, what constraints must it satisfy to function properly? Make a list, and we'll revisit this list in Section~\ref{sec:door-design-intent}.

## Turning the Hinge into an Assembly

Before modeling the door, let's get the hinge in order. Download the \solidworks file for McMaster PN [XXX](https://www.mcmaster.com/XXX/) and move it to your working directory. On opening it, we find that this single part contains the full hinge assembly (two leafs plus a pin). This is a multi-body part, which we encountered briefly in Section~\ref{sec:incomplete}. It is built in the same fashion as single-body parts, except that the features were selectively merged. Let's navigate through the feature tree to investigate how these bodies came about.

#### Flat feature trees and Dynamic Visualization
First, flatten the feature tree using *Part Tree Options > Flatten feature tree*, found by right-clicking on the part name. **VERIFY THIS** Sketches are now un-absorbed from features, and any folders are temporarily removed. I use flat feature trees at times, especially for trouble-shooting broken parts.

The upside of this view is that we can see the order that \solidworks uses when creating the part. The downsides include:

- We can't put the features into folders to improve organization.
- Large parts become cluttered and unwieldy.
- We lose the connection between sketches and features.

I recommend fixing the last of these problems by turning on *Dynamic Visualization of Parents* and *Dynamic Visualization of Children*, both found by right-clicking on **FINISH THIS**.

![](images/figures/dynamic-visualization-menu.png)

With these options turned on, mousing over a feature or sketch will highlight the items on which the feature/sketch depends (the parents, in XXX) and the items which *directly* depend on the feature/sketch (the children, in XXX). I keep both of these features on at all times in my personal work.

![](images/figures/dynamic-visualization.png)

#### The Rollback Bar & Merging Features

At the bottom of the feature tree is the rollbak bar. Grabbing the rollback bar, we can display the part in partially built states. This is useful for both understanding how a part is created and for adding sketches & features mid-way through the feature tree.

![](images/figures/rollback-bar-1.png)

Roll back below Extrude XX, which created the first leaf. At this stage, there is only one body. Editing \cadsymbol{Edit-Feature} this feature, we see that this extrude doesn't have a merge option because, prior to its creation, there were no solid bodies. **Verify this**. Close this feature.

![](images/figures/hinge-rollback-1.png)

Move the rollback bar below Extrude XX, the starting feature of the second leaf. This feature is not merged with any bodies, and as a result, our body count changes from one to two following this feature.

![](images/figures/hinge-rollback-2.png)

Close this feature and finally edit \cadsymbol{Edit-Feature} Extrude XX, which creates XXX. This feature has the merge option selected, meaning that it adds to an existing body rather than creating a new body. However, the designer chose to merge it with only a single body, rather than all bodies. If you intend to selectively merge a feature (including subtractive features like Extrude-Cut), I recommend avoiding "Auto-Select" Feature Scope, and instead select the affected bodies yourself. 

### Building the Hinge Assembly
\label{sec:build-hinge-assembly}

Let us now return to our goal of building a hinge assembly that moves as a hinge should. Our strategy is to create two new parts, one for each leaf, and combine these into an assembly file.

#### Add Reference Geometry

From the \relation{Reference-Geometry} menu, create a new \relation{Axis}. There are many ways to define axis, but we use the intersection of two planes. Select both the *Front?* and *Top?* planes \cadsymbol{green-check}. Drag the created axis from its current position to the top of the feature tree, below the *Origin*. This will make it easier to find when we use it in an assembly. Rename the axis as *Hinge Axis*. 

![](images/figures/new-hinge-axis.png)

I've burned myself before by making axes that aren't in fact concentric with the intended features. The easiest way to confirm concentricity is via the \relation{Measure} tool. Within Measure, select the *Hinge Axis* and one of the pin's cylindrical faces. The tool will measure the displacement between the selected axes which, if all has gone to plan, are concentric (Figure~\ref{fig:hinge-concentricity}).

![\label{fig:hinge-concentricity}](images/figures/hinge-concentricity.png)

\questiontriangle If I wanted the hinge axis to be concentric with the hinge pin, why not define it as such when creating the new axis? Why define it from the cardinal planes instead?

#### Three Flavors of Save As

From the hinge file, select \relation{Save-As}. \solidworks Save As dialog presents three options:

![](images/figures/save-as-menu.png)

**Save As**: This option creates a new file and updates all existing references (say from assemblies and drawings) to the new file. I find this option is dangerous because I may be updating files that I didn't know exist[^where-used].

[^where-used]: We can find out where a file is used via the *Where Used* utility, found XXX.

**Save Copy & Open**: This option creates a new file without updating any references in existing files. The new file and the old file both remain open.

**Save Copy & Continue**: This option also creates a new file without updating references. As opposed to "Save Copy & Open", this option closes the new file. Think of it as creating a snapshot and putting that file in the archives. 

Because there are no references to the hinge, it doesn't matter which we choose, so we'll stick with the default. Save the file as *XXX*. 

#### Delete/Keep Bodies

Within the new file, add a \relation{Delete-Keep-Bodies} feature. This feature does as the name implies. Choose the "Keep Bodies" option & select one leaf \cadsymbol{green-check}. The file now contains all of the information to create the full hinge, but only this selected leaf remains.

Return to the original file and add a \relation{Delete-Keep-Bodies} feature to this part as well. Keep the other hinge leaf and the pin. This file still maintains the original file name. We will rename it in Section~\ref{sec:rename-hinge-leaf}.

![](images/figures/delete-keep-body-hinge.png)

### Make the Hinge Assembly

Create a new \relation{Assembly}. Before dropping in the parts, create a hinge axis within the assembly in the same fashion as we did in Section~\ref{sec:build-hinge-assembly}. \relation{Insert} both hinge leafs and *Float* the fixed one (see Section~\refben.smith@neptunemedical.com{sec:fixed-and-floating-parts} if needed).

\questiontriangle What are the benefits of creating all these hinge axes? When would it be a waste of time?

Choose one leaf and constrain its position in a method you see fit. You could mate the part and assembly origins, as in Section~\ref{sec:constrain-base-part}. There are many other strategies that work. Confirm the part and assembly hinge axes are aligned, and the part is fully constrained. 

Next, mate the floating leaf as a hinge is actually mated. A nice feature of adding the hinge axes to the leaf parts and the assembly is that we can make these axes \mate{Coincident}, and our hinge is automatically aligned. 

Adding the *Hinge Axes* also communicates to others (and our future selves) how parts can interface with this assembly. Should we need to add a part concentric to the hinge axis (perhaps an automatic door opener) in the future, we can do it by locating any one of the hinge axes.

Regarding the question above, adding hinge axes to the individual leafs doesn't make sense if we're still choosing from one of many hinge options. It only makes sense once we're confident in hinge choice (or, perhaps, the hinge has been decreed). At the assembly level, I'd argue it almost always makes sense add the hinge axis.

### Renaming Parts with Existing References

Our hinge assembly is now complete. Let's rename the one leaf from the Windows File Explorer. Normally, we can rename a file with *Right-Click > Rename*. The problem with doing so here is that no existing references within the assembly will update[^reference-update].

[^reference-update]: I welcome you to try it. Change the filename. Open the assembly in SolidWorks. You'll be met with a message "Unable to locate the file C:\...\PT-00XXX.SLDPRT. Would you like to find the file yourself?" You'll have 10 frantic seconds to read the message, remember which part is problematic, and choose between the three options. I recommend ignoring the urge to panic, letting the timer expire, then fix the broken part from the Part Tree.

\solidworks{} provides a utility for renaming files. On my Windows 11 operating system, it is located by right-clicking on the file, then *Show more options > \solidworks{} > Rename...*.

![](images/figures/rename-utility-location.png)

The utility finds and updates all existing references to the file. We will explore a more efficient way of renaming files in Section~\ref{sec:rename-files-from-part-tree}.