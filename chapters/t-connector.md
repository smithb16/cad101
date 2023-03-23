# A First Useful Part

The widget we built in Chapter~\ref{chapter:modifying-first-widget} is unique in that it has no constraints. It didn't have to fit in a hand, or bolt to a motorcycle, or be injection-moldable. Unless you're designing abstract art[^abstract-art], your designs will be subject to constraints[^no-constraints]. These can come in the form of interfacing parts (e.g. the aforementioned bolts and motorcycle), natural constraints (e.g. the human hand), or manufacturing limitations (e.g. draft angles in molding, minimum radii in machining).

[^no-constraints]: Fully-custom unmanned satellites are probably a close second for fewest constraints.

[^abstract-art]: I've surely lost an abstract artist from my readership now.

If we design our parts well, our constraints will be explicit and defined in one place. When the constraints change (which they surely will, perhaps that same Director of Marketing), a well-built model is easy to update and robust to parameter changes. Such is our task in this chapter.

## A Tee Connector

Our goal is to design a bracket that will connect two aluminum extrusion rails[^8020] in a Tee fashion, as shown in Figure~\ref{fig:starting-rails}. Our process will be roughly as follows. This process will work will with most of the parts you ever design.

[^8020]: Commonly called 80/20\texttrademark\  extrusions after the company that makes them, 80/20, Inc.

1. Define the constraints (Section~\ref{sec:define-constraints}).
2. Design a part that works with those constraints(Section~\ref{sec:build-tee-connector}).
3. Build the part into an assembly (Section~\ref{sec:first-assembly}).
4. Add finishing touches to the part (Section~\ref{sec:finishing-touches}).

### Define the Constraints
\label{sec:define-constraints}
\questiontriangle What are the constraints that define our bracket? I'd argue there are three main ones.

The constraints on are bracket are:

1. The geometry of the horizontal rail.
2. The geometry of the vertical rail (which happens to be the same as the horizontal rail).
3. The fact that we want to arrange the rails in a Tee fashion.

Visiting the McMaster-Carr page for Part Number [47065T503](https://www.mcmaster.com/47065T503-47065T1/), we are greeted by a list of component specifications. I'd argue the critical dimensions are those highlighted in Figure~\ref{fig:rail-specifications}, rail height (1'') and T-slot width (0.256'').

![\label{fig:rail-specifications}](images/figures/rail-specifications.png)

Identifying critical dimensions is often the easy part of defining the constraints. The more challenging part is incorporating those constraints into our parts, and we'll take that on in Section~\ref{section:sketching-the-constraints}.

Before we leave, let's download the 3-D \solidworks file from McMaster. One of the most powerful aspects of McMaster is the depth of their CAD files, from [screws](https://www.mcmaster.com/91251A190/) to [saws](https://www.mcmaster.com/7159K21/) to [speed limit signs](https://www.mcmaster.com/5940T42/).

### Sketching the Constraints
\label{sec:bracket-sketching-constraints}

Open a new part and \relation{Save} it as ``PT-02 - Extrusion Bracket''. Create a sketch on the *Front Plane*. Our eventual constraint sketch is shown in Figure~\ref{fig:bracket-constraint-sketch}, but let's start by drawing the rectangular profiles, as in Figure~\ref{fig:bracket-constraint-rectangles}. In doing this, one useful tool is \relation{Select-Midpoint}, found by right-clicking on the line. Once a midpoint is selected, we can additionally select the origin and either make the two points \relation{Coincident} or \relation{Vertical} to one another.

![fig:bracket-constraint-sketch](images/figures/bracket-constraint-sketch.png)

![fig:bracket-constraint-rectangles](images/figures/bracket-constraint-rectangles.png)

\questiontriangle Why are we constraining the midpoint of these lines to be vertical with the *Origin*?

Looking at our finished part in Figure~\ref{fig:bracket-completed}, we see that the *Right Plane* (and consequently the origin) is a plane of symmetry for our part. Therefore, we'll design all of our sketches with left-to-right symmetry.

Using \relation{Equal} relations, make the rectangles the same size in both heigt and length. Rather than adding this relation in the standar fashion, let's use a hotkey in the following manner.

- Select both entities to display the relations menu.
- Hold \texttt{Alt} to underline a set of letters in the *Relations* menu.
- Still holding \texttt{Alt}, add the relation by pressing the underlined letter (in this case \texttt{q})

We need two dimensions to define the current set of entities. One is the rail length, which we can set arbitrarily[^arbitrary-length] at 3''.

[^arbitrary-length]: For we can cut the rails as long or short as we'd like.

The other dimension is rail height, which we identified in Section~\ref{sec:define-constraints} as 1''. When we add this dimension, we should also add a note in the dimension text, calling out this dimension as ``Rail Height''.

![](images/figures/bracket-dimension-text.png)

Next, let's define the fastener size used with these rails. I've done so as shown in Figure~\ref{fig:bracket-fastener-sketch} by these steps:

1. Add a construction line to the center of one rail.
2. Parallel to the construction line, add a line to represent one side of the rail fastener slot.
3. Using the Mirror Entity tool, mirror the solid line about the construction line. If we select both and then click \relation{Mirror-Entity}, the tool assumes we want to mirror the solid line about the construction line and does so automatically.
4. Add a dimension between the two solid lines. Set this dimension to *0.256''*, and label this dimension as ``slot width''.

\questiontriangle Why haven't we added a fastener slot to both the horizontal and vertical rails?

We only need a fastener slot on one rail because, in our current plans, the fasteners will all be the same size. When we draw the fastener holes later in Section~\ref{fig:bracket-fastener-holes}, we only need to constrain one hole with this slot, and all others can be made equal.

The geometry sketch is now complete. Close the sketch \cadsymbol{green-check}. Because this sketch is so central to our part, I like to rename it from the Feature Tree to something like "Rail Geometry". When another user picks up this part to change, say, the rail size, this sketch stands out more than "Sketch 2". The easiest way to rename a sketch is to select the sketch and press \texttt{F2}. *Click-pause-click* strategy also works but is more finnicky.

### Design the Part
\label{sec:design-the-part}

Even though we've only defined our constraints, Step 1 of our Four-Step Program, we've also completed the hardest part. The world is now our oyster, and any design that satisfies the geometric constraints from Section~\ref{sec:bracket-sketching-constraints} is acceptable. Three possible designs are shown in Figure~\ref{fig:bracket-three-designs}. For simplicity, we'll make the left-most design.

![Three designs that satisfy the constraints for our tee bracket. \label{fig:bracket-three-designs}](images/figures/bracket-three-designs.png)

Make a new \relation{Sketch} on the *Front Plane*. Start by drawing the three holes as in Figure~\ref{fig:bracket-hole-sketch}. 

![\label{fig:bracket-hole-sketch}](images/figures/bracket-hole-sketch.png)

\questiontriangle Why only draw half of the outline?

We're designing a bracket that's symmetrical about the *Right Plane*. We could draw and specify this symmetry (with constraints and dimensions), or we could have \solidworks give it to us for free. If we draw both sides of the outline, its up to us to make sure left and right sides are equal. However, if we draw one side and later mirror the entire part (Section~\ref{sec:bracket-mirror-part}), we're guaranteed that left and right sides are equal. That is the option I've chosen for us.

Before we worry about the outline of our bracket, let's size and position those circles. Make them all equal by drag-selecting them (Box~\ref{aside:selection-strategies}) and making them \relation{Equal}. Add the dimensions shown in Figure~\ref{fig:bracket-hole-dimensions}. Finally, make one circle tangent to the fastener slot, which sizes the circles according to the dimension we set in Section~\ref{sec:bracket-sketching-constraints}.

![\label{fig:bracket-hole-dimensions}](images/figures/bracket-hole-dimensions.png)

Next, add the bracket outline as shown in Figure~\ref{fig:bracket-outline-sketch}[^bracket-off-script]. When you draw this outline, many horizontal, vertical, and coincident relations are automatically added. I encourage you to move slowly in this step to confirm any auto-created relations are desired.

[^bracket-off-script]: If you'd like to go off-script with a different bracket outline, I won't stop you. I do recommend sticking with a symmetric outline.

In Figure~\ref{fig:unintended-relation}, we have the classic "relation you didn't want". This occurs when \solidworks makes line's endpoint coincident with a different line far away. Preventing this unintended relation is easier than troubleshooting after-the-fact.

![\label{fig:unintended-relation}](images/figures/unintended-relation.png)

### Add the Holes

**TODO** add the holes using convert entities.

### Dimensioning the Bracket

We are now at the point where additional relations won't help to define the bracket, and its time to add dimensions. I like to ask myself "What do I care about?" when I'm adding dimensions. Three options for dimensioning the outline are shown in Figure~\ref{fig:bracket-dimensioning}.

\questiontriangle What are the benefits and weaknesses of each dimensioning scheme?


#### Scheme A - Overall Envelope Defined

![\label{fig:bracket-dimensioning}](images/figures/bracket-dimensioning.png)

This scheme is useful if we want strict control of the overall dimensions, perhaps because our manufacturing method has a maximum part size. One downside is that if we made the model with larger holes, or moved the holes farther apart, they could easily move outside the border, breaking the part.

#### Scheme B - Define Hole Center to Edge

![\label{fig:bracket-dimensioning}](images/figures/bracket-dimensioning.png)

This sche is useful if we're using manual fabrication techniques and aim to minimize math used in the layout process. This dimensioning scheme says "Scribe your edge. Measure 1/2" in and up, and makr your hole location there." A downside is that if th eholes grow in diameter, they reduce the wall thickness, potentially to zero!

#### Scheme C - Define from Hole Edge to Part Edge

![\label{fig:bracket-dimensioning}](images/figures/bracket-dimensioning.png)

The strength of this dimensioning scheme is that it preserves the part's intent (holes in a plate) regardless of the hole size or spacing. We will always have 1/8" of wall thickness around our holes. The downside of this scheme is that we can end up with overall part dimensions less easily measured by a ruler. (The part envelope of the component as drawn is XXX" x XXX").

Because so much of modern manufacturing is computer-controlled, it is less important to have clean numbers in our envelope dimensions or hole spacings. I find **Scheme C** is often preferable, and it is the one we will implement.

#### Dimensioning to Hole Edges

But wait, you protest, when I click the perimeter of the cercile, the dimension snaps to the center! It sure does. If you hold \texttt{Shift} while clicking the circle, the dimension attaches to the perimeter, definining either a minimum distance from circle to edge or, if you click the circle's far perimeter, the maximum distance from circle to edge (less useful).

![\label{fig:circle-to-edge-dimensions}](images/figures/circle-to-edge-dimensions.png)

Choosing between the three dimensioning schemes is our first example of expressing **design intent**, a declaration of what we care about in our design. None of the options were right or wrong, and in other instances, Options A or B may be preferable. And please don't preach that Option C is always preferable, because that would be incorrect.

Once we've added all dimensions in Figure~\ref{fig:bracket-dimensions}, we're now left with the task of turning our half-sketch into a full part.

### Extrude the Half-Sketch

Start by extruding the sketch created in Section~\ref{sec:bracket-design}. It seems reasonable to choose an off-the-shelf thickness for our extrusion, so I've chosen 3/16". Because the bracket is symmetric front-to-back, I'll argue that a *Mid-Plane* extrude is preferable to a *Blind* extrude, because this kees the origin on a plane of symmetry. (This is the answer to Exercise 3 in Section~\ref{sec:modify-widget-exercises}). Close the extrude dialog \cadsymbol{green-check} to get a half-plate.

![\label{fig:half-plate-extrude}](images/figures/half-plate-extrude.png)
\begin{aside}
\label{aside:adding-appearance}
\heading{Adding an Appearance}

This is a test.

\end{aside}

### Holes, Please

**TODO: Figure out how we want to design the holes. Recommend adding them to the profile sketch, then getting them for free in the extrude.**

### Mirror the Body
Finally, lets use \relation{Mirror} to turn our half-bracket into a full bracket. Because we want to mirror the entire part, choose *Body Mirror* from the feature dialog[^body-mirror]. Select the *Right Plane* as the mirror plane. Confirm that "Merge results" is select, lest we end up with two half-brackets.

[^body-mirror]: Suppose you were to accidentally use a *Feature mirror*, close the dialog box, then wish to change the feature to a *Body mirror*. For a reason that I cannot explain, the *Body mirror* option disappears. You will need to delete and remake the mirror feature to access the *Body mirror* option.

If all has gone to plan, we have a bracket that will connect our extrusions as intended. Quite franky, I'm never confident my part will work until I see all the parts connected in an assembly. We'll do that in Chapter~\ref{cha:bracket-assembly}. But first, \relation{Save} your part.