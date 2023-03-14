# Modifying our Part 

## (The Wrong Way)

If all has gone to plan, your part currently looks like Figure~\ref{fig:exercise-1-widget}. Let's now suppose we want to make it look like Figure~\ref{fig:exercise-1-widget-mod}, perhaps by decree of the Director of Marketing, who said the last design was too ``static''. Easy enough, we'll just tilt one leg and call it a day.

![\label{fig:exercise-1-widget}](images/figures/exercise-1-widget.png)

![\label{fig:exercise-1-widget-mod}](images/figures/exercise-1-widget-mod.png)

Start by editing the sketch now absorbed in *Extrude 1*, probably called *Sketch 1*. Delete the vertical leg and reposition the hypotenuse, which is now under-constrained. Add a new line back to the origin. Select both lines and add a perpendicular relation so that the horizontal line is now the hypotenuse. With the sketch again fully defined, close the sketch \cadsymbol{close-sketch}.

On doing so, you will probably find that you were met by a series of error messages, and your feature tree looks like a construction zone. What went wrong?

### The Problem

When \solidworks creates a face, that face is defined, for example, as "the face formed by extruding Line 1 from Sketch 1''. If you \relation{Edit} the Triangle sketch, you can right-click on the newest line and \relation{Select-Other}. The line is probably titled *Line 4*, not *Line1*, *Line 2*, or *Line 3*[^line-names]. When we updated the sketch, we had no way to tell \solidworks that *Line4* is the new *Line1*. Thus, anything depending one *Line1* is now broken.

[^line-names]: \solidworks numbers lines, sketches, features, and all other entities sequentially. You may have drawn extra lines, and therefore have numbers beyond *Line4*. The most recently drawn line should still have the largest number.

XX TODO can we locate the place where this definition comes from?XX

### The Fix

Let us now practice a skill more valuable than doing things right, the skill of fixing things done wrong. We'll follow a three-step protocol which works well in most computer applications.

1. Actually read the error message.
2. Interpret the error message.
3. Address the error.

Because features (*Revolve1*) depend on sketches (*Revolve Sketch*), let's start with the errors in *Revolve Sketch*.

\begin{quote}
\coloredtext{red}{Warning...}
\end{quote}

Editing *Revolve Sketch* shows two relations now in a foul yellow color[^foul-color]. Delete these relations by selecting them, followed by \texttt{Delete}[^led-astray]. Drag the end of the construction line back to the midpoint to re-create the relation. Do the same with the corner of the rectangle. The sketch is again *Fully Defined*. Close the sketch \cadsymbol{close-sketch}.

[^led-astray]: The last time I told you to blindly delete the sketch line, I intentionally led you astray. I'm not doing that here. Deleting sketch relations is the correct way to modify sketches.

[^foul-color]: Closest Pantone color: XXXXX

Now for the next error message:

\begin{quote}
\coloredtext{red}{Warning: Could not find face or plane.}
\end{quote}

\( \vartriangleright \) Which face or plane can \solidworks not find?

The face referenced here is the face that *Revolve Sketch* lives on. as indicated by the fact that our half-cyclinder is now floating in space:

![](images/figures/floating-half-cylinder.png)

Right-clicking on *Revolve Sketch*, we can \kode{Edit Sketch Plane} \cadsymbol{edit-sketch-plane} and select the desired face. When we close \cadsymbol{green-check} the dialog box, we should be back in business. Now that *Revolve Sketch* is error-free, *Revolve1* is also error-free.

Our academic widget is now complete, and with our new skills, we can begin to build parts that serve a function. \relation{Save} the part, and let's move on.

## Exercies

1. Edit the part back into its first rendition, where the horizontal base was a leg and not the hypotenuse. Do this only by adding and deleting sketch relations. Confirm that the part rebuilds as desired.

2. Edit *Triangle Sketch* and add an unsolvable relation. The sketch should now be *Over-Defined* and contain lots of red. What error messages do you get? ![](images/figures/over-defined-triangle.png)

3. Our CAD is sloppy in that we've designed a part that is symmetric about a plane, but none of our cardinal planes align with that plane of symmetry. Fix this. Hint: fixing this problem should require no math.