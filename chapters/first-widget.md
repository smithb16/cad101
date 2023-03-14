# Our First Widget

In this chapter, we'll make our very first part together, the basic and not-at-all-useful part shown in Figure \ref{fig:}. This part will allow us to experiment, making the part, breaking the part, and changing the part, all without the fear that we'll jeopardize project timelines or make unfixable errors. By chapter's end, you should know how to:
- Build a simple part
- Add that part into a drawing
- Modify the part without breaking it

![\label{fig:first-widget}](../images/figures/first-widget.png)

## Making a Triangle

Open SolidWorks and create a new part using the default part template:

![](../images/figures/default-part-template.png)

We are presented with a Feature Tree, menu tabs, working area, and potentially a few toolbars, as in Figure~\ref{fig:working-view}.

![\label{fig:working-view}](../images/figures/empty-solidworks.png)

Our first task is to create the triangular cross-section shown in Figure \ref{fig:first-sketch-triangle}. Start by creating a new \relation{Sketch} on the *Front Plane*. Use the \relation{Line} tool to create three lines forming a triangle. If you've successfully closed the triangle, the Line tool will automatically exit.

![\label{fig:first-sketch-triangle}](images/figures/first-sketch-triangle.png)

A few points are worth noting regarding this sketch.

- If you haven't changed it, your view is called an Isometric view. "Iso" (Greek \ref{fig:}, or equal), "metric" (Greek \ref{fig:}, or measure), meaning that a line will display the same length regardless of its sketch plane. We can identify this by the coordinate system.

![](../images/figures/coordinate-system-isometric.png)

-  Alignment guides (Figure~\ref{fig:sketch-alignment-guides}) appear, say if we are vertically above the origin. The guides make it easier to create our sketch geometry, but sometimes they do things we don't want. If we want to over-ride their power, we can hold *Control* while we draw.

- Relations (Figure~\ref{fig:sketch-alignment-guides}) appear beside the cursor when drawing lines. Yellow relations are added to the sketch, whereas white relations are merely "for your information". Relations will be discussed in Section~\ref{sec:}.

![\label{fig:sketch-alignment-guides}](../images/figures/sketch-alignment-guides.png)

Once we have a triangle (any triangle), close the sketch. We will now turn the part from a 2D sketch into a 3D feature using Extrude[^pasta1]. Select \relation{Extrude} from the feature tab, select the triangle sketch (probably called *Sketch1*), and set the extrude distance to 1", as in Figure~\ref{fig:first-extrude-dialog}. If your default length units are anything besides inches, see Aside~\ref{aside:part_units}.

[^pasta1]: As in pasta.

![\label{fig:first-extrude-dialog}](../images/figures/first-extrude-dialog.png)

You should now have something that resembles Figure~\ref{fig:simple-widget-first-extrude}. Congratulations! You've made your first part. Because we aren't working in the cloud, now is a great time to \relation{Save}.

![\label{fig:simple-widget-first-extrude}](../images/figures/simple-widget-first-extrude.png)

When choosing a part name, I recommend adopting a part numbering scheme. Throughout this book, I'll use the scheme in Figure \ref{fig:}, which makes this part *PT-001 - Simple Widget*.

\begin{aside}
\label{aside:part_units}
\heading{Changing Part Units}

\noindent SolidWorks plays well with most length units from small to large, provided the dimensions remain within the scale of manmade objects. SolidWorks' units are defined in *Options > Document Properties > Units*.
![](../images/figures/unit-settings.png)

However, the easiest way to change the part's units are with the dropdown menu in the part's bottom-right. We will work in Imperial units (inch, pound, second) for this tutorial, not because I think it is better (I don't), but it is more confusing and will allow for more teaching opportunitites.

![](../images/figures/units-dropdown.png)

Shoud you want to change the units of a single dimension, you can do so by overriding the default units. If you do this, I recommend modifying the *Dimension Text* to include the units.

![](../images/figures/units-override.png)

![](../images/figures/units-dimension-text.png)

\end{aside}

## Modifying our Part

Throughout this chapter, we'll commit a number of poor CAD practices, for this will set us up for learning opportunities. We have committed the first already, so let's fix it.

The problem is that *Sketch1* is under-defined, meaning our triangle is not defined to a certain size and shape. We can tell this because:

- The sketch entities (lines in this case) are highlighted blue.
- If we grab one of the triangles endpoints, we can move it.
- There is a (-) next to the sketch name.
- The "Under Defined" at the bottom of the sketch window.

![\label{fig:under-defined-sketch}](../images/figures/under-defined-sketch.png)

Under-defined sketches have fewer constraints than degrees of freedom. In simpler terms, this means that we can still move things around. We can see this by editing Sketch 1 **Edit Sketch**. If you haven't already, drag and drop one vertex of our triangle to the sketch origin. Doing so creates a **Coincident** relation between the origin and the vertex.

A three-step process is necessary to view the relations (which in this instance is academic, but will later be critical):
1. Edit the sketch. Relations are only visible while editing sketches.
1. Select the *Hide All Types* dropdown and select *View Sketch Relations*.
![\label{fig:view-sketch-relations}](../images/figures/view-sketch-relations.png)
1. Confirm the *Hide All Types* eyeball is not depressed.
![\label{fig:hide-all-types}](../images/figures/hide-all-types.png)

![\label{fig:triangle-one-relation}](../images/figures/triangle-one-relation.png)

### What is a Relation?
There are two ways for us to specify the geometry of sketches. One is with dimensions (say 1" or 15 degrees). Relations are ways for us to specify the geometry of sketches without the use of numbers. One line, for instance, can be constrained vertically. Two lines can be constrained parallel to each other, perpendicular to each other, equal in length, or along the same line (collinear). Each relation is represented by a symbol near the affected entities. A full table of SolidWorks relations is shown in Appendix~\ref{app:relations}.

Next, we'll turn our triangle into a right triangle. Add a horizontal relation to one leg by this process:

* Select the leg
* Select \relation{Horizontal} in the Sketch Entity sidebar

Add a \relation{Perpendicular} relation to the pair of legs connected to the origin[^perpendicular]. I'll encourage you to figure out how to select multiple lines, but for more information, see Aside~\ref{aside:selection-strategies}.

[^perpendicular]: Yes, a vertical relation on a single leg would suffice, but this allows for an extra teachable moment. In practice, a vertical relation would be perfectly acceptable.

We now have a right triangle. Both legs are constrained in orientation and they are no longer blue. However, their endpoints are blue, menaing we can change their length. Likewise, we can change the length and orientation of the hypotenuse, which is fully blue. We will now use dimensions to fully define our sketch.

### Adding Dimensions

Use the \kode{Smart} \relation{Dimension} tool to make the hypotenuse 2'' long. You could add this dimension in one of two ways:

1. Select the line.
1. Select both endpoints of the line.

For 95% of my needs, Option 1 is both simpler and more appropriate. I'll let you discover places to leverage Option 2 on your own. [^imperial-units]

[^imperial-units]: If you weren't born into a former British colony, my use of inches may be annoying. Feel free to substitute your favorite unit of length. \solidworks doesn't much care. Later exercises, where we use off-the-shelf hardware, won't be so foregiving.

Add an angular dimension between the horizontal leg and the hypotenuse in the same fashion. When the \relation{Dimension} tool is activated, we don't need to use \texttt{Ctrl} to multi-select. We can simply click on entities to select them, and use \texttt{Esc} to cancel the selection. Place the angular dimension inside the triangle to specify an interior angle.

Congratulations, our sketch is now fully defined, as noted in the bottom of the screen. Exit the sketch. The extrusion will automatically update. Now is a great time to \relation{Save}.

### Adding a Revolve

Extrudes are one of the most common features in part design, useful when we sweep a cross-sectional sketch along an axis perpendicular to that sketch[^sweep].
In our industrial world, as opposed to the natural world, many parts are rotationally symmetric. For those, we need the \relation{Revolve} feature. Let's add a revolve to the side of our existing widget.

[^sweep]: For non-perpendicular axes, we can use the \relation{Sweep} feature.

From our extrude, we get five new faces on which to sketch, in addition to the three cardinal planes (*Front*, *Top*, and *Right*). Select the vertical face and create a \kode{New} \relation{Sketch}. Sketch the entities shown in Figure~\ref{fig:revolve-sketch}. The rectangle will become the cross-section of the half-cylinder. Create this rectangle either by drawing four connected lines or with one of the \relation{Rectangle} tools.

![\label{fig:revolve-sketch}](images/figures/revolve-sketch.png)

We need to tell \solidworks which axis to revolve our rectangle about, for the same rectangular cross-section can produce infinite toroids (Figure~/ref{fig:toroids}).

![\label{fig:toroids}](images/figures/toroids.png)

If our sketch contains one closed contour (the rectangle) and one construction line, \solidworks will interpret the construction line as the axis of revolution[^centerline]. Construction lines are lines that help specify geometry, but they are not used as contours when generating features (Figure~\ref{fig:construction-lines-to-triangle}). 

[^centerline]: \solidworks uses the term \relation{Centerline} for construction geometry. However, this tool is useful even if the line isn't in the center. For this reason, I'll use the term \kode{Construction Line}.

![I can add construction lines to the triange sketch from Figure~\ref{fig:first-sketch-triangle}, but I still get the same old prism. \label{fig:construction-lines-to-triangle}](images/figures/construction-lines-to-triangle)

There are two ways of creating construction lines, and I use both frequently.

1. Draw a standard line. Select that line, and check ``For construction''. This strategy works not just for lines, but for arcs, splines, hexagons, etc.
1. Select the dropdown beside \relation{Line}, and choose \relation{Centerline}.

![\label{fig:centerline-to-rectangle}](images/figures/centerline-to-rectangle)

Add a \constructionline down the middle of the face as in Figure~\ref{fig:centerline-to-rectangle}. Make one endpoint coincident with the edge's midpoint, and confirm that the construction line is \relation{Vertical}. Note that the sketch is *Fully Defined* even though we haven't constrained the length of the construction line.

Last time, we colsed the sketch before making our extrude. However, that was unnecessary. We can choose the \relation{Revolve} feature, and \solidworks will assume we wish to revolve the currently opened sketch. Change the revolve angle to 180\textdegree to prevent the toroid from bulging through the backside. If necessary, use *Change Directions* to modify the direction. Close the feature \cadsymbol{green-check}. Our part is now complete!

Before we move on, find the sketch that we just created. Rename this sketch *Revolve Sketch*.