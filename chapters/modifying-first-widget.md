# Modifying our Part 
\label{chapter:modifying-first-widget}

If all has gone to plan, your part currently looks like Figure~\ref{fig:exercise-1-widget}. Let's now suppose we want to make it look like Figure~\ref{fig:exercise-1-widget-mod}, perhaps by decree of the Director of Marketing, who said the last design was too ``static''. Easy enough, we'll just tilt one leg and call it a day.

![\label{fig:exercise-1-widget}](images/figures/first-widget-alt.png)

![\label{fig:exercise-1-widget-mod}](images/figures/first-widget-mod.png)

## The Wrong Way

Start by editing *Triangle Sketch* \cadsymbol{edit-sketch}, now absorbed in *Triangle Extrude*. Delete the vertical leg and reposition the hypotenuse, which is now under-constrained.

![](images/figures/triangle-delete-leg.png)

Add a new line back to the origin. Select both lines and add a perpendicular relation so that the horizontal line is now the hypotenuse.

![](images/figures/triangle-mod-constrained.png)

With the sketch again fully defined, close the sketch \cadsymbol{close-sketch}. On doing so, you will probably find that you were met by a series of error messages, and your feature tree looks like a construction zone. This part is definitely not what the Director of Marketing is looking for. What went wrong?

![](images/figures/broken-feature-tree.png)

![\label{fig:broken-feature-tree} A broken feature tree generally produces a broken part.](images/figures/widget-broken.png)

### The Problem

When \solidworks creates a face, that face is defined, for example, as "the face formed by extruding *Line2* from *Triangle Sketch* ". If you \relation{Edit} *Triangle Sketch* and double-click on the \relation{Perpendicular} symbol, you can see the name of the entities constrained by the relation[^line-names]. 

![](images/figures/entity-names.png)

When we updated the sketch, we had no way to tell \solidworks that *Line18* is the new *Line1*. In other words, we should've modified the sketch without deleting any lines. Anything depending one *Line1* is now broken.

[^line-names]: \solidworks numbers lines, sketches, features, and all other entities sequentially. You may have drawn extra lines, and therefore have numbers beyond *Line4*. The most recently drawn line should still have the largest number.

### The Fix

Let us now practice a skill more valuable than doing things right, the skill of fixing things done wrong. We'll follow a three-step protocol which works well in most computer applications.

1. Actually read the error message.
2. Interpret the error message.
3. Address the error.

Because features (e.g. *Revolve*) depend on sketches (*Revolve Sketch*), let's start with the errors in *Revolve Sketch*. Error messages are visible by mousing over the highlighted text or by right-clicking on the problem sketch and selecting "What's Wrong?"

\begin{quote}
\coloredtext{orange}{This sketch contains dimensions or relations to model geometry which no longer exists.}
\end{quote}

Editing *Revolve Sketch* shows three relations now in a foul yellow color[^foul-color]. Delete these relations by selecting them and pressing \texttt{delete}[^led-astray].

![](images/figures/revolve-sketch-broken-relations.png)

Drag the end of the construction line back to the midpoint to re-create the \relation{Midpoint} relation. Do the same with the corners of the rectangle to remake the \relation{Coincident} relations. 

![](images/figures/revolve-sketch-fixed-relations.png)

The sketch is again *Fully Defined*. Close the sketch \cadsymbol{close-sketch}.

[^led-astray]: The last time I told you to blindly delete the sketch line, I intentionally led you astray. I'm not doing that here. Deleting sketch relations is the correct way to modify sketches and rarely has unintended side effects.

[^foul-color]: Closest Pantone color: 104 C

Now for the next error message, also on *Revolve Sketch*:

\begin{quote}
\coloredtext{orange}{Warning: Could not find face or plane.}
\end{quote}

\questiontriangle Which face or plane can \solidworks not find?

The face referenced here is the face that *Revolve Sketch* lives on, as indicated by the fact that our half-cyclinder is now floating in space.

Right-clicking on *Revolve Sketch*, we can \kode{Edit Sketch Plane} \cadsymbol{edit-sketch-plane} and we find the sketch plane is currently designated \coloredtext{orange}{**Missing Face<1>**}. Select the desired sketch face. When we close \cadsymbol{green-check} the dialog box, we should be back in business. Now that *Revolve Sketch* is error-free, *Revolve* is also error-free.

![](images/figures/first-widget-mod.png)

Our academic widget is now complete, and with our new skills, we can begin to build parts that serve a function. \relation{Save} the part, and let's move on.

## Exercies
\label{sec:modify-widget-exercises}

1. Edit the part back into its first rendition, where the horizontal base was a leg and not the hypotenuse. Do this only by adding and deleting sketch relations. Confirm that the part rebuilds as desired.

2. Edit *Triangle Sketch* and add an unsolvable relation, such as making another set of legs perpendicular. The sketch should now be *Over-Defined* and contain lots of red. What error messages do you get? 

![](images/figures/over-defined-triangle.png)

3. Our CAD is sloppy in that we've designed a part that is symmetric about a plane, but none of our cardinal planes align with that plane of symmetry. Fix this without the use of math.

4. Create a new sketch in a new part. Sketch four lines to form a rectangle.
    - Constrain these four lines using only dimensions. You can leave any horizontal and vertical relations that were auto-generated.
    - Delete all but one dimension. Use only relations to fully define the sketch.
    - Add an arc to each side of the square. Using only relations, make these four arcs into a continuous circle.

![](images/figures/rectangle-exercise.png)