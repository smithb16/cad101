# A First Useful Part
\label{cha:tee-connector}

The widget we built in Chapter~\ref{chapter:modifying-first-widget} is unique in that it has no constraints. It didn't have to fit in a hand, or bolt to a motorcycle, or be injection-moldable. Unless you're designing abstract art[^abstract-art], your designs will be subject to constraints[^no-constraints]. These can come in the form of interfacing parts (e.g. the aforementioned bolts and motorcycle), natural constraints (e.g. the human hand), or manufacturing limitations (e.g. draft angles in molding, minimum radii in machining).

[^no-constraints]: Fully-custom unmanned satellites are probably a close second for fewest constraints.

[^abstract-art]: I've surely lost an abstract artist from my readership now.

If we design our parts well, our constraints will be explicit and defined in one place within the CAD model. When the constraints change (which they surely will, another decree by that same Director of Marketing), a well-built model is easy to update and robust to parameter changes. Such is our task in this chapter.

Our goal is to design a bracket that will connect two aluminum extrusion rails[^8020] in a Tee fashion, as shown in Figure~\ref{fig:finished-tee-assembly}.

[^8020]: Commonly called 80/20\texttrademark\  extrusions after the company that makes them, 80/20, Inc.

![\label{fig:finished-tee-assembly}](images/figures/finished-tee-assembly.png)

## A Tee Connector

### Aluminum Extrusion Rails

Extrusion rails are the classic way to build adjustable structures. They are often used in prototyping while the final design is uncertain. More and more, rail systems are making their way in to final products.

![](images/figures/rails-in-final-products.png)

Rails come in metric and imperial sizes ranging from 10mm (1/2") to 160mm (6"), and along with the [rails](https://8020.net/framing-options.html), 80/20, Inc has a full ecosystem of [fasteners](https://8020.net/fasteningmethods.html), [brackets](https://8020.net/fasteningmethods/externalfasteners/bracketsgussetscorners.html), and [accessories](https://8020.net/addoncomponents.html). This includes a version of the [bracket](https://www.mcmaster.com/47065T278/) we will be designing.

![](images/figures/extrusion-profiles.png)

### A General Process
\label{sec:four-step-program}

The process described below will take us from goal to CAD model. This process will work will with most of the parts you ever design.

1. Define the constraints (Section~\ref{sec:define-constraints}).
1. Create sketches that capture those constraints (Section~\ref{sec:bracket-sketching-constraints})
2. Design a part that works with those constraints(Section~\ref{sec:design-the-part}).
3. Build the part into an assembly (Chapter~\ref{cha:tee-bracket-assembly}).
4. Add finishing touches to the part (Section~\ref{sec:finishing-touches}).

### Define the Constraints
\label{sec:define-constraints}
\questiontriangle What are the constraints that define our bracket? I'd argue there are three main ones.

The constraints on are bracket are:

1. The geometry of the horizontal rail.
2. The geometry of the vertical rail (which happens to be the same as the horizontal rail).
3. The fact that we want to arrange the rails in a Tee fashion.

\questiontriangle Of the rail geometry called out in Figure~\ref{fig:rail-specifications}, which dimensions are important to us? Which can we ignore?

![\label{fig:rail-specifications} Component drawing from McMaster PN \href{https://www.mcmaster.com/47065T503-47065T563/}{47065T563}](images/figures/rail-specifications.png)

I'd argue the critical dimensions are those highlighted in Figure~\ref{fig:rail-specifications}, rail height (1'') and T-slot width (0.256''). In this case, we aren't using the center hole. We also don't care at this stage that the rail is a given length.

Identifying critical dimensions is often the easy part of defining the constraints. The more challenging part is incorporating those constraints into our parts, and we'll take that on in Section~\ref{sec:bracket-sketching-constraints}.

#### Download the Rail
One of the most powerful aspects of McMaster is the depth of their CAD files, from [screws](https://www.mcmaster.com/91251A190/) to [saws](https://www.mcmaster.com/7159K21/) to [speed limit signs](https://www.mcmaster.com/5940T42/). Before we leave the McMaster page, let's download the *3-D \solidworks{}* file from McMaster. If it ends up in your *Downloads* folder, I recommend moving it to your working directory. 

![](images/figures/mcmaster-rail-download.png)

### Sketching the Constraints
\label{sec:bracket-sketching-constraints}

Open a new part and \relation{Save} it as ``PRT-002 - Extrusion Bracket''. Create a sketch on the *Front Plane*. Our eventual constraint sketch is shown in Figure~\ref{fig:bracket-constraint-sketch}, but let's start by drawing the rectangular profiles, as in Figure~\ref{fig:bracket-constraint-rectangles-no-centerline}. 

![\label{fig:bracket-constraint-sketch}](images/figures/bracket-constraint-sketch.png)

In doing this, one useful tool is \kode{Select Midpoint}, found by right-clicking on a line. Once a midpoint is selected, we can additionally select the origin and make the two points either \relation{Coincident} or \relation{Vertical} to one another.

![\label{fig:bracket-constraint-rectangles-no-centerline}](images/figures/bracket-constraint-rectangles-no-centerline.png)

\questiontriangle Why are we constraining the *Origin* along the center of the rectangles, rather than on the left or right edge?

Looking at our finished part in Figure~\ref{fig:finished-tee-assembly}, we see that the *Right Plane* (and consequently the origin) is a plane of symmetry for our part. Therefore, we'll design all of our sketches with left-to-right symmetry.

Using \relation{Equal} relations, make the rectangles the same size in both height and length. Rather than adding this relation as we have before, let's use a hotkey in the following manner.

- Select both entities by holding the \texttt{ctrl} key. This displays the relations menu.
- Note that in the **Add Relations** menu, each option has an underlined letter.
- While holding \texttt{alt}, add an \relation{Equal} relation by pressing the underlined letter (in this case \texttt{q}).

Finally, add a \relation{Centerline} along the major axis of each rectangle to arrive at Figure~\ref{fig:bracket-constraint-rectangles}.

![\label{fig:bracket-constraint-rectangles}](images/figures/bracket-constraint-rectangles.png)

#### Dimension Text

We need two dimensions to define the current set of entities. One is the rail length, which we can set arbitrarily[^arbitrary-length] at 4''.

[^arbitrary-length]: For we can cut the rails as long or short as we'd like.

The other dimension is rail height, which we identified in Section~\ref{sec:define-constraints} as 1''. When we add this dimension, we should also add a note in the dimension text, calling out this dimension as ``Rail Height''.

![](images/figures/bracket-dimension-text.png)

Next, let's define the fastener size used with these rails. I've done so as shown in Figure~\ref{fig:bracket-fastener-sketch} by these steps:

1. Add a construction line to the center of one rail.
2. Parallel to the construction line, add a line to represent one side of the rail fastener slot.
3. Using the Mirror Entity tool, mirror the solid line about the construction line. If we select both and then click \relation{Mirror-Entity}, the tool assumes we want to mirror the solid line about the construction line and does so automatically.
4. Add a dimension between the two solid lines. Set this dimension to *0.256''*, and label this dimension as ``slot width''.

![\label{fig:bracket-fastener-sketch} Similar to adding comments to code, adding labels to dimensions will facilitate future part handoffs. More often than not, it will help you pick up the part in the future.](images/figures/bracket-fastener-sketch.png)

\questiontriangle Why haven't we added a fastener slot to both the horizontal and vertical rails?

We only need a fastener slot on one rail because, in our current plans, the fasteners will all be the same size. When we draw the fastener holes later in Section~\ref{sec:bracket-fastener-holes}, we only need to constrain one hole with this slot, and all others can be made equal.

The geometry sketch is now complete. Close the sketch \cadsymbol{green-check}. Because this sketch is so central to our part, rename it from the Feature Tree to *Rail Geometry*. When another user picks up this part to change, say, the rail size, this sketch stands out more than *Sketch 2*.

![](images/figures/bracket-constraint-with-feature-tree.png)

### Design the Part
\label{sec:design-the-part}

Even though we've only defined our constraints, Step 1 of our Four-Step Program (Section~\ref{sec:four-step-program}), we've also completed the hardest part. The world is now our oyster, and any design that satisfies the geometric constraints from Section~\ref{sec:bracket-sketching-constraints} is acceptable. Three possible designs are shown in Figure~\ref{fig:bracket-three-designs}. For simplicity, we'll make the left-most design.

![Three designs that satisfy the constraints for our tee bracket. \label{fig:bracket-three-designs}](images/figures/bracket-three-designs.png)

#### Sketch the Holes

Make a new \relation{Sketch} on the *Front Plane*. Start by drawing the three holes as in Figure~\ref{fig:bracket-hole-sketch}. 

![\label{fig:bracket-hole-sketch}](images/figures/bracket-hole-sketch.png)

Note that when we draw the circles, we are able to auto-constrain the center to be \relation{Coincident}, as indicated by the yellow symbol. However, we cannot auto-constrain a \relation{Tangent} relation, as indicated by the white "For Your Information" symbols.

![](images/figures/circles-added-relations.png)

Before we worry about the outline of our bracket, let's size and position those circles. Make them all equal by drag-selecting them (Box~\ref{aside:selection-strategies} for more details) and making them \relation{Equal}. Add the dimensions shown in Figure~\ref{fig:bracket-hole-dimensions}. Finally, make one circle \relation{Tangent} to the fastener slot, which sizes the circles according to the dimension we set in Section~\ref{sec:bracket-sketching-constraints}.

![\label{fig:bracket-hole-dimensions}](images/figures/bracket-hole-dimensions.png)

\questiontriangle What's up with the **2"** dimension? How do we make it? Why is it preferred to a dimension between the a circle and the centerline (which would measure *1"*)?

Whenever a sketch has a centerline, we can create dimensions either to that centerline:

![](images/figures/dimension-to-centerline.png)

Or mirrored across the centerline:

![](images/figures/dimension-across-centerline.png)

Often, reflecting the dimension across the centerline makes sense when we are specifying a radially symmetric part where we care about the diameter. In this case, we can specify the hole spacing, which makes more sense than the half-hole spacing.

We make this dimension by selecting the circle and centerline, then placing the dimension on the far side of the centerline.

#### Outline the Half Bracket

Next, add the bracket outline as shown in Figure~\ref{fig:bracket-outline-sketch}[^bracket-off-script]. When you draw this outline, many horizontal, vertical, and coincident relations are automatically added. I encourage you to move slowly in this step to confirm any auto-created relations are desired.

![\label{fig:bracket-outline-sketch}](images/figures/bracket-outline-sketch.png)

\questiontriangle Why only draw half of the outline?

We're designing a bracket that's symmetrical about the *Right Plane*. We could draw and specify this symmetry (with constraints and dimensions), or we could have \solidworks{} provide it for free. If we draw both sides of the outline, its up to us to make sure left and right sides are equal. However, if we draw one side and later mirror the entire part (Section~\ref{sec:bracket-mirror-part}), we're guaranteed that left and right sides are equal. That is the option I've chosen for us.

[^bracket-off-script]: If you'd like to go off-script with a different bracket outline, I won't stop you. I do recommend sticking with a symmetric outline.

### Dimensioning the Bracket

We are now at the point where additional relations won't help to define the bracket, and its time to add dimensions. I like to ask myself "What do I care about?" when I'm adding dimensions. Three options for dimensioning the outline are shown in Figure~\ref{fig:bracket-dimensioning}.

\questiontriangle What are the benefits and weaknesses of each dimensioning scheme?


#### Scheme A - Overall Envelope Defined

![](images/figures/bracket-dimensioning-overall-envelope.png)

This scheme is useful if we want strict control of the overall dimensions, perhaps because our manufacturing method has a maximum part size. One downside is that if we made the model with larger holes, or moved the holes farther apart, they could easily move outside the border, breaking the part.

![](images/figures/bracket-dimensioning-overall-envelope-large-hole.png)

#### Scheme B - Define Hole Center to Edge

![](images/figures/bracket-dimensioning-hole-center-to-edge.png)

This scheme is useful if we're using manual fabrication techniques and aim to minimize math used in the layout process. This dimensioning scheme says "Scribe your edge. Measure 1/2" in and up, and make your hole location there." A downside is that if the holes grow in diameter, they reduce the wall thickness, potentially to zero!

![](images/figures/bracket-dimensioning-large-hole-center-to-edge.png)

#### Scheme C - Define from Hole Edge to Part Edge

![\label{fig:bracket-dimensioning-hole-edge-to-edge}](images/figures/bracket-dimensioning-hole-edge-to-edge.png)

The strength of this dimensioning scheme is that it preserves the part's intent (holes in a plate) regardless of the hole size or spacing. We will always have 1/8" of wall thickness around our holes. The downside of this scheme is that we can end up with overall part dimensions less easily measured by a ruler.

Because so much of modern manufacturing is computer-controlled, it is less important to have clean numbers in our envelope dimensions or hole spacings. I find **Scheme C** is often preferable, and it is the one we will implement.


![](images/figures/bracket-dimensioning-large-hole-edge-to-edge.png)

#### Dimensioning to Hole Edges

But wait, you protest, when I click the perimeter of the circle, the dimension snaps to the center! It sure does. If you hold \texttt{Shift} while clicking the circle, the dimension attaches to the perimeter, defining either a minimum distance from circle to edge or, if you click the circle's far perimeter, the maximum distance from circle to edge (less useful).

![\label{fig:circle-to-edge-dimensions} By holding \texttt{Shift} while clicking the circle, we can dimension the minimum distance (black) or maximum distance (grey) from the circle to edge.](images/figures/circle-to-edge-dimensions.png)

Choosing between the three dimensioning schemes is our first example of expressing **design intent**, a declaration of what we care about in our design. None of the options were right or wrong, and in other instances, Options A or B may be preferable. And please don't preach that Option C is always preferable, because that would be incorrect.

Once we've added all dimensions in Figure~\ref{fig:bracket-dimensioning-hole-edge-to-edge}, we're now left with the task of turning our half-sketch into a full part.

#### Cleanup with Trim

Our sketch currently has multiple closed contours (Figure~\ref{fig:multiple-closed-contours}). If we were to extrude the sketch as-is, \solidworks{} wouldn't know which contours should be the positive space and which should be the holes. Therefore, we should do some cleanup. I like to make cleanup my last sketch before extruding the bracket.

![\label{fig:multiple-closed-contours} The current sketch has multiple closed contours, and it is unclear to \solidworks{} which outline is desired. \solidworks{}, however, has no problem with an isolated hole in a plate.](images/figures/multiple-closed-contours.png)

Use the \relation{Trim} tool. Set the trim option as *Trim to closest*. Select the lines as in Figure~\ref{fig:bracket-trim-lines} to arrive at an outline with a single outline profile.

![\label{fig:bracket-trim-lines}](images/figures/bracket-trim-lines.png)

### Extrude the Half-Sketch

Start by extruding the sketch created in Section~\ref{sec:bracket-design}. It seems reasonable to choose an off-the-shelf thickness for our extrusion, so I've chosen 3/16". Because the bracket is symmetric front-to-back, I'll argue that a *Mid-Plane* extrude is preferable to a *Blind* extrude, because this keeps the origin on a plane of symmetry. (This is the answer to Exercise 3 in Section~\ref{sec:modify-widget-exercises}). Close the extrude dialog \cadsymbol{green-check} to get a half-plate.

![\label{fig:half-plate-extrude}](images/figures/half-plate-extrude.png)

\begin{aside}
\label{aside:adding-appearance}
\heading{Adding an Appearance}

This is a test.

\end{aside}

### Mirror the Body
Finally, lets use \relation{Mirror} to turn our half-bracket into a full bracket. Because we want to mirror the entire part, choose *Body Mirror* from the feature dialog[^body-mirror]. Select the *Right Plane* as the mirror plane. Confirm that "Merge results" is select, lest we end up with two half-brackets.

[^body-mirror]: Suppose you were to accidentally use a *Feature mirror*, close the dialog box, then wish to change the feature to a *Body mirror*. For a reason that I cannot explain, the *Body mirror* option disappears. You will need to delete and remake the mirror feature to access the *Body mirror* option.

If all has gone to plan, we have a bracket that will connect our extrusions as intended. Quite frankly, I'm never confident my part will work until I see all the parts connected in an assembly. We'll do that in Chapter~\ref{cha:tee-bracket-assembly}. But first, \relation{Save} your part.

![\label{fig:full-plate-extrude}](images/figures/full-plate-extrude.png)
