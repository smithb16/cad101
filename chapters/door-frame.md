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

With the hinge dimensioned, we are left with one under-defined sketch feature, the distance between the door's unhinged side and the frame. The most common way to constrain this missing dimension is to say "I bet a quarter inch is enough clearance." and add that dimension, as in Figure~\ref{fig:constrain-gap-distance}. But we can do better.

![\label{fig:constrain-gap-distance}](images/figures/constrain-gap-distance.png)