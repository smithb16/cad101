# Our First Widget
## Chapter 1

In this chapter, we'll make our very first part together, the basic and not-at-all-useful part shown in Figure XX. This part will allow us to experiment, making the part, breaking the part, and changing the part, all without the fear that we'll jeopardize project timelines or make unfixable errors. By chapter's end, you should know how to:
- Build a simple part
- Add that part into a drawing
- Modify the part without breaking it

Open SolidWorks and create a new part using the default part template:

![](../Images/default-part-template.png)

We are presented with a Feature Tree, menu tabs, working area, and potentially a few toolbars, as in Figure XX.

![](../Images/empty-solidworks.png)

Our first task is to create the triangular cross-section shown in Figure XX. Start by creating a new sketch on the Front Plane. Use the Line tool to create three lines forming a triangle. If you've successfully closed the triangle, the Line tool will automatically exit. A few points are worth noting regarding this sketch.

- If you haven't changed it, your view is called an Isometric view. "Iso" (Greek XX, or equal), "metric" (Greek XX, or measure), meaning that a line will display the same length regardless of its sketch plane. We can identify this by the coordinate system.
  - ![](../Images/coordinate-system-isometric.png)

-  Alignment guides (Figure XX) appear, say if we are vertically above the origin. The guides make it easier to create our sketch geometry, but sometimes they do things we don't want. If we want to over-ride their power, we can hold *Control* while we draw.

- Relations (Figure XX) appear beside the cursor when drawing lines (Figure XX). Yellow relations are added to the sketch, whereas white relations are merely "for your information". Relations will be discussed in Section XX.

![](../Images/sketch-alignment-guides.png)

Once we have a triangle (any triangle), close the sketch. We will now turn the part from a 2D sketch into a 3D feature using Extrude. Select Extrude from the feature tab, select the triangle sketch (probably called *Sketch1*), and set the extrude distance to 1", as in Figure XX. If your default length units are anything besides inches, see Aside XX.

![](../Images/first-extrude-dialog.png)

You should now have something that resembles Figure XX. Congratulations! You've made your first part. Because we aren't working in the cloud, now is a great time to Save.

![](../Images/simple-widget-first-extrude.png)

When choosing a part name, I recommend adopting a part numbering scheme. Throughout this book, I'll use the scheme in Figure XX, which makes this part *PT-001 - Simple Widget*.

#### Aside:

SolidWorks plays well with most length units from small to large, provided the dimensions remain within the scale of manmade objects. SolidWorks' units are defined in *Options > Document Properties > Units*.
![](../Images/unit-settings.png)

However, the easiest way to change the part's units are with the dropdown menu in the part's bottom-right. We will work in Imperial units (inch, pound, second) for this tutorial, not because I think it is better (I don't), but it is more confusing and will allow for more teaching opportunitites.

![](../Images/units-dropdown.png)

Shoud you want to change the units of a single dimension, you can do so by overriding the default units. If you do this, I recommend modifying the *Dimension Text* to include the units.

![](../Images/units-override.png)

![](../Images/units-dimension-text.png)

## Modifying our Part

Throughout this chapter, we'll commit a number of poor CAD practices, for this will set us up for learning opportunities. We have committed the first already, so let's fix it.

The problem is that *Sketch1* is under-defined, meaning our triangle is not defined to a certain size and shape. We can tell this because:
- The sketch entities (lines in this case) are highlighted blue.
- If we grab one of the triangles endpoints, we can move it.
- There is a (-) next to the sketch name.
- The "Under Defined" at the bottom of the sketch window.

![](../Images/under-defined-sketch.png)

Under-defined sketches have fewer constraints than degrees of freedom. In simpler terms, this means that we can still move things around. We can see this by editing Sketch 1 **Edit Sketch**. If you haven't already, drag and drop one vertex of our triangle to the sketch origin. Doing so creates a **Coincident** relation between the origin and the vertex.

A three-step process is necessary to view the relations (which in this instance is academic, but will later be critical):
1. Edit the sketch. Relations are only visible while editing sketches.
1. Select the *Hide All Types* dropdown and select *View Sketch Relations*.
![](../Images/view-sketch-relations.png)
1. Confirm the *Hide All Types* eyeball is not depressed.
![](../Images/hide-all-types.png)

![](../Images/triangle-one-relation.png)

### What is a Relation?
There are two ways for us to specify the geometry of sketches. One is with dimensions (say 1" or 15 degrees). Relations are ways for us to specify the geometry of sketches without the use of numbers. 