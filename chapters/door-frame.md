# Door Frame & Assembly
\label{cha:door-frame}

We are now ready to build our door-frame system. In this chapter, we'll learn the powerful techniques of:

- Using sketches to assess and specify motion (Section~\ref{sec:})
- Creating a multi-body model (Section~\ref{sec:})

Our process will be as follows:

1. Sketch the geometry of the door, frame, and hinge within a single Part file (Section~\ref{sec:})
2. Turn those sketches into solid bodies (Section~\ref{sec:})
3. Break this multi-body part out into part files containing only a single body (Section~\ref{sec:})
4. Build an assembly of the parts and confirm we've achieved our goals (Section~\ref{sec:})

By the end of this chapter, we'll have a door assembly that moves as a door should and is easily configurable to different hinges or door sizes. More importantly, the process we'll go through is highly scalable to much more complicated assemblies. I get paid to use these same techniques with 20+ custom parts. I hope these techniques will take you far.

## Geometry Sketches

As we did in Section~\ref{sec:} when developing the extrusion bracket, our first step is to sketch the critical geometry of our parts in 2-D. We will eventually end up with two geometry sketches, one from the top view and one from the front view, as in Figure~\ref{fig:door-geometry-sketches}.

![\label{fig:door-geometry-sketches}](images/figures/door-geometry-sketches.png)

\questiontriangle Why don't we need a right view of the door geometry?
\questiontriangle Which sketch should we start with, the front or the top sketch?

We can start with either the top view or the right view. I like to ask myself, "Which view feels most useful without feeling too intimidating?" In this case, the top view, which contains information about the frame, hinge, and door motions, is the most informative. Sometimes, such a sketch, containing motion and many parts, will make my brain hurt, so I start with an easier sketch.

First, draw a cross-sectional sketch of the door within the frame. This will show the door in the closed position. Dimension the sketch as in Figure~\ref{fig:door-cross-section-sketch}. Note that the sizes of all the rectangles are defined, but their positions are not.

![\label{fig:door-cross-section-sketch}](images/figures/door-cross-section-sketch.png)

Below, I've added construction lines to show which lines are collinear. While there's no need to add these lines, make sure you've mated the frame rectangles to be equal and horizontal with each other.

![\label{fig:door-cross-collinear}](images/figures/door-cross-collinear.png)

Next, add a cross-section of the hinge in the closed position. Referencing my front door, the hinge will look like this:

![](images/figures/door-hinge-cross-section.png)

Hinge critical dimensions are found on the [McMaster Page](FIX ME).

With the hinge dimensioned, we are left with one under-defined sketch feature, the distance between the door's unhinged side and the frame. The most common way to constrain this missing dimension is to say "I bet a quarter inch is enough clearance." Add that dimension, as in Figure~\ref{fig:constrain-gap-distance}.

\questiontriangle Why is this bad practice?

![\label{fig:constrain-gap-distance}](images/figures/constrain-gap-distance.png)

The problem is that this method of problem solving is not scalable. In other words, while we may get away with it in this case, that is only because we're familiar with doors and their dimensions. When we're contracted to design new doors for, say, your local bank vault, that 1/4" clearance won't cut it. Let's demonstrate that.

### Specifying Design Intent in Door Clearance

One magical feature of CAD is that we can specify the door clearance in a method that captures our design intent. And we can do so without performing any math! Our strategy will be to sketch the path of the door as it pivots about its hinges. From that virtual path, we can then define the minimum clearance distance.

Start by sketching a circle concentric with the hinge center. Make the circle's perimeter coincident with the corner of the door furthest from the hinge.

![](images/figures/door-pivot-circle.png)

Note that the closest point of contact is between the door's corner and the frame's corner. This is the distance we want to control so that it never goes below zero. Such a condition would cause door interference.

\questiontriangle How do we dimension the distance from this point to the arc of the door's motion?

One way to dimension the gap to the door's arc is to add a circle around the door frame vertex as in Figure~\ref{fig:door-clearance-circle}. Make this circle tangent to the door's arc. By dimensioning the circle's radius, we can set the gap. Add a \relation{dimension} to the circle's diameter, and change it to a radius dimension by *Right-Click > Display Options > Display as Radius*. I would also label this radius as "Door Gap" and set it to a distance that feels right, perhaps 0.1".

![\label{fig:door-clearance-circle}](images/figures/door-clearance-circle.png)

## Breaking Out Bodies
\label{sec:break-out-bodies}

Once our multi-body part is built, wer're left to break out the bodies into individual part files. There are a few reasons this is preferred to leaving them grouped together:

- In an assembly, only parts from different part files can be moved with respect to each other.
- Drawings are cleaner when working with a single-body part file, even though we *can* display a single body within a multi-body part drawing.
- We can move some features (especially aesthetic features like child part chamfers and fillets) from the parent file to the child part file, thus de-cluttering the parent feature tree.

There are XX ways to transition from a multi-body part to many single-body parts. The only method I trust is implemented here. Other methods are covered in Section~\ref{sec:save-bodies} & Section~\ref{sec:XXX} as a cautionary overview.

### Insert Part and Keep Bodies
\label{sec:keep-bodies}

My preferred method for breaking multi-body parts into part files leverages the Keep Bodies feature, the same one we used in Section~\ref{sec:XXX}. Though its not perfect (problems covered in Section~\ref{sec:keep-bodies-problems}), it's the most stable method I've encountered. If it does break, it does so in a generally repairable fashion.

We will now make a part file containing only the door frame. Create a \relation{New} part file and, if necessary, choose from your favorite part template. \relation{Save} this file as *PRT-XXX - Door Frame*. Insert the parent part file (*PRT-XXX - FILENAME*) by using *Insert > \relation{Part}*. From the feature dialog box, select the part (or browse if its not already open).

![](images/figures/insert-part.png)

Unlike inserting a part into an assembly, clicking in the working area doesn't arbitrarily locate the part. Instead, it places the child part origin coincident with the parent part origin. From the feature dialog, we can choose which entities to import from the parent body. I generally limit the selection to *Solid Bodies, Axes, and Hole Wizard Data*. If we want other features later (say planes), we can edit the Insert Part feature as we would any other feature.

![](images/figures/insert-part-dialog.png)

We now have a parent part file (PRT-XXX - ) and a child part file (PRT-XXX - PRT-XXX - Door Frame) with identical bodies. Add a \relation{Keep-Bodies} feature to keep only a single body, in this case the door frame. I prefer the "Keep Bodies" option to the "Delete Bodies" option because, should I add another body to the base part, I won't need to update the Keep Bodies feature. \relation{Save} the part.

![](images/figures/keep-bodies-door-frame.png)

### Creating a Break Out Bodies Macro
\label{sec:create-macro}

You could imagine that executing this process for tens of bodies would be repetitive, boring, and error-prone. When I hear those words, I think "Sounds like a great job for a computer." We'll now walk through the process of creating the macro in Box~\ref{code:breakout-bodies-macro}.

\begin{codelisting}
\label{code:breakout-bodies-macro}
\codecaption{Break Out Bodies Macro}
```
Sub ExportFlatPattern(part As SldWorks.PartDoc, flatPattern As SldWorks.Feature, outFilePath As String, opts As SheetMetalOptions_e, conf As String)
    
    Dim swModel As SldWorks.ModelDoc2
    Set swModel = part
    
    Dim error As ErrObject
    Dim hide As Boolean

try_:
    
    'On Error GoTo catch_

```
\end{codelisting}

**RESTART HERE**

### What about Save Bodies?
\label{sec:save-bodies}

In theory, the \relation{Save-Bodies} feature is the perfect tool for this task. It creates a new file and adds only the bodies we choose to that file.

![](images/figures/save-bodies.png)

Most mechanical designers who use this method are eventually burned when the feature fails and disassociates from all child files. This ruins assemblies and drawings. That is the reason we haven't employed Save Bodies here.

## Door Assembly

We will now assemble the door, frame, and hinge. In building the assembly, we can finally assess if our design is successful. 

\questiontriangle Below, I'll walk through the assembly process. But you, an intelligent human with multiple assemblies under your belt, should give it your best shot first. Get as far as you can on your own and then reference the text. Our final assembly is shown in Figure~\ref{fig:door-final-assembly}.

![\label{fig:door-final-assembly}](images/figures/door-final-assembly.png)

Make a new \relation{Assembly} file. Insert these files:

- PRT-XXX
- PRT-XXX
- ASM-XXX

As always, *Float* the first part you added.

\questiontriangle What is a reasonable choice for the assembly origin? In other words, how should we locate the *Top*, *Right*, and *Front Plane*?

I'll argue that the ground is a great location for the *Top Plane* To achieve this, make the bottom of the door frame and the assembly *Top Plane* \relation{Coincident}. Then, rename the *Top Plane* as "Ground Plane".

![](images/figures/door-ground-plane.png)

I'll also argue that there are multiple sensible choices for locating the *Front* and *Right* planes. I've shown two in Figure~\ref{fig:door-multiple-origins}. Locating the origin isn't about winning, it's about not losing. As long as we're intentional in our choices, we've avoided losing and we need not stress.

![\label{fig:door-multiple-origins}](images/figures/door-multiple-origins.png)

For this lesson, we'll keep consistent and place a hinge axis between the *Front* and *Right Planes*.

![](images/figures/door-assembly-hinge-axis.png)

### Constraining the Remainder of the Components

Because of this choice, we can find the hinge axis from each component and make it \relation{Coincident} with the top-level assembly's *Hinge Axis*. Do this with the frame, door, and hinge assembly.

![](images/figures/component-coincident-hinge-axes.png)

\questiontriangle What is our current problem list with the assembly? Which things can move in ways they shouldn't?

Currently, the door frame is under-constrained, as it is prefixed with "(-)". Last I checked, door frames shouldn't move. Add relations to correct this as you see fit.

Additionally, the door can move up and down. Again, not good. In real life, the hinges are used to prevent vertical door movement. However, CAD is not real life, and we don't have to build the door that way.

**Restart Here**