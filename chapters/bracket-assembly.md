# Bracket Assembly
\label{cha:tee-bracket-assembly}

In this chapter, we'll take the bracket from Chapter~\ref{cha:tee-connector}, two segments of extrusion, and some fasteners and build them into a digital assembly. This will help tell us with greater certainty whether our design has accomplished our goals.

## A New Assembly

Create a new assembly. When the file opens, we are met with the "Insert Parts" dialog box. Since we're planning to insert multiple parts, pin \cadsymbol{Pin} the dialog. Insert the tee connector (*PRT-002 - Extrusion Bracket*) by selecting it from the menu, then clicking in the design space.

![\label{fig:first-assembly-insert-parts} Populate the parts in random locations. Depending on your display settings, un-hidden sketches may show when the part is inerted. We'll take care of these in Section~\ref{sec:assembly-hide-sketches}.](images/figures/first-assembly-insert-parts.png)

Repeat the insertion process with two extrusions (McMaster PN [47065T503](https://www.mcmaster.com/47065T503-47065T1/)). Using the download process from Section~\ref{sec:define-constraints}, download a screw (McMaster PN [90909A526](https://www.mcmaster.com/90909A526/)) and a t-slot nut (McMaster PN [47065T905](https://www.mcmaster.com/47065T905/)). Add both in quantity one to the assembly. Per our naming convention, \relation{Save} this assembly as *ASM-001 - Extrusions + Bracket*.

### Fixed and Floating Parts
\label{sec:fixed-and-floating-parts}

With the parts populated, we will use mates to define their orientation in the assembly. As constraints are to a 2D sketch, mates are to a 3D assembly. In the parts tree, with one exception, all parts have the prefix "(-)", meaning they are not fully constrained and can be moved around. The first part we dropped into the assembly has the prefix "(f)", meaning it is fixed in space. This is unfortunate because it is fixed in a random location, potentially far from the assembly's origin. Right-click on this fixed part and select \kode{Float}.

![\label{fig:first-assembly-part-tree} The part tree after inserting all components. The "(f)" prefix appears on the first part dropped into the assembly, though I recommend Floating the part and positioning it on your own.](images/figures/first-assembly-part-tree.png)

## Adding Mates

**TODO: Add paragraph regarding mates**

### Constrain a Base Part
\label{sec:constrain-base-part}

Our next task is to constrain the assembly. First, let's choose one base part and fully constrain it in our assembly. This part will then act as the foundation for all other parts. The foundation part should be a part that:

1. Doesn't move with respect to the assembly (*i.e.* no rotating or translating)
2. Serves a prominent role in the assembly (*i.e.* don't choose the screw)

Let's choose the plate (PRT-002 from Chapter~\ref{cha:tee-connector}) as our foundation part. Using the \relation{Mate} tool, add a \mate{Coincident} mate between the part origin and the assembly origin, as in Figure~\ref{fig:bracket-assembly-origin}. 

![\label{fig:bracket-assembly-origin} When selecting construction geometry (\textit{e.g.} planes, axes, origins) for mating, I navigate via the auxiliary part tree which appears.](images/figures/bracket-assembly-origin.png)

With this one mate, our part is fully constrained. The "(-)" prefix has disappeared. We cannot drag the part around. Note that this mate is now in our part tree in two locations, once under the part and once under the list of assembly mates. The mate also has the Ground symbol \cadsymbol{Ground}, meaning it contributes to grounding this part within the assembly.

![](images/figures/mate-twice-in-part-tree.png)

### Hiding and Showing Parts

**TODO:** Write section using \texttt{Tab} to hide & show parts.

### Position the Horizontal Rail

Next, mate the horizontal rail. I prefer to mate parts when they're in roughly the correct orientation, rather than floating randomly in space. Use the \relation{Triad} tool to move the rail near the plate, as in Figure~\ref{fig:bracket-rail-approximate-position}.

![\label{fig:triad-options} The triad arrow translates the part along the assembly major axis. The rings rotate the part about the assembly major axis. Inside the rings, the discs translate the part on a plane. Right-clicking on the triad presents some useful options.](images/figures/triad-options.png)

With the rail oriented, it is easier to see which planes and faces we should mate together to constrain the rail. 

![\label{fig:bracket-rail-approximate-position}](images/figures/bracket-rail-approximate-position.png)

\questiontriangle Which mate(s) are needed to constrain the horizontal rail?

Unfortunately, constraining origins won't give the results we're after. Doing this would create interference between the plate and the rail, as well as orient the rail incorrectly.

![](images/figures/bracket-rail-origin-interference.png)

Three coincident mates are needed to locate the rail.

\begin{center}
\begin{tabular}{cc}
  \hline
  \mate{Coincident} & \includegraphics[height=60mm]{images/figures/bracket-coincident-1.png} \\
  \mate{Coincident} & \includegraphics[height=60mm]{images/figures/bracket-coincident-2.png} \\
  \mate{Coincident} & \includegraphics[height=60mm]{images/figures/bracket-coincident-3.png} \\
  \hline
\end{tabular}
\end{center}

While you can open the \relation{Mate} toolbar to generate these images, I prefer the following strategy for any of the standard mates:

1. Select the first mate entity.
2. Holding \texttt{ctrl}, select the second mate entity.
3. Select the desired mate from the toolbar that appears. ![](images/figures/pop-up-mate-toolbar.png)
4. If the toolbar disappears and you want it back, mouse over the area where it was and press \texttt{ctrl}.


Repeat the same process with the second, vertical rail to arrive at Figure~\ref{fig:bracket-assembly-rails-oriented}. At this point, we can confirm (or deny) that the bracket achieved the goal of orienting the rails as intended.

![\label{fig:bracket-assembly-rails-oriented}](images/figures/bracket-assembly-rails-oriented.png)

## Adding One Fastener

While the big pieces of the assembly are now in place, it is incomplete until we put the fasteners in. All of the fasteners. I'm opinionated on this matter because I've burned myself too many times by trying to cut corners. Here's a few reasons I populate all fasteners in my models:

1. If your fasteners don't fit and you have to hand-modify hardware, these modifications can dominate your assembly time.
2. If you populate all fasteners, \solidworks{} can automatically generate an accurate Bill of Materials (BOM).
3. Assessing tool access to each fastener is challenging unless the fastener is present. Our minds are not good at filling in the missing parts.

With philosophy out of the way, let's take action. First, let's get the screw in place with these mates:

\begin{center}
\begin{tabular}{cc}
  \hline
  \mate{Concentric} & \includegraphics[height=60mm]{images/figures/screw-concentric-1.png} \\
  \mate{Coincident} & \includegraphics[height=60mm]{images/figures/screw-coincident-1.png} \\
  \hline
\end{tabular}
\end{center}

If your parts are oriented as mine are, you will end up with a screw pointing the wrong way:

![\label{fig:screw-wrong-way} Because the screw started off in the wrong orientation, it will mate by default in the wrong orientation. The mottled appearance of the screw head is \solidworks{}' telltale sign of interference, which is obvious here but valuable in other instances.](images/figures/screw-wrong-way.png)

When adding either the concentric or coincident mate, select \kode{Flip Mate Alignment} \cadsymbol{flip-mate-alignment} to orient the screw correctly. Should you want to flip the mate later, locate the mate in the part tree, right-click, and *Flip Mate Alignment*.

![](images/figures/flip-mate-alignment-menu.png)

Repeat the same steps to locate the T-nut on the fastener. I'll let you decide which mates are needed. While there is no sense in constraining the screw in rotation, we should constrain the nut rotation, perhaps with a \mate{Parallel} or \mate{Perpendicular} mate. Otherwise, it may poke through the extrusion rail.

![\label{fig:t-nut-rotation} Rotate the t-nut within the rail to get rid of the interference. Rotating the T-nut not only improves our CAD cleanliness, but it allows us to answer the question "Does the T-nut stick out the bottom of the rail?" In this case, the T-nut is tangent to the bottom of the rail.](images/figures/t-nut-rotation.png)


## More Fasteners
\label{sec:copy-with-mates}

Now that we've specified one fastener set, we can easily get more. While there are many ways we can duplicate the fastener sets, we will copy the components.

From the Part Tree, select both the nut and screw. *Right-click* on one and \kode{Copy with Mates}\cadsymbol{copy-with-mates}. By copying both parts at once, they are duplicated as a set. For any mates that we want to re-use exactly (as in our coincident mates), check the "Repeat" box. For others, such as the concentric and parallel mates, select the hole or face that we want to use instead. 

![](images/figures/copy-with-mates-menu.png)

Doing so will create a new fastener set, and the dialog will remain open to create more sets until we close it \cadsymbol{red-x}.

![](images/figures/copy-with-mates-complete.png)

With the fasteners installed, our assembly is complete. Congratulations! In the exercises, we will break, fix, and modify the assembly. However, because of the way we've designed and assembled the plate, we will never have to rebuild the parts from ground zero. 

## Reviewing the Assembly

As stated in the Introduction (Chapter~\ref{cha:introduction}), one of the great powers of CAD is that we can visualize and review assemblies long before we spend money on parts. We will now step through that process. My version of the assembly review process is captured in Box~\ref{aside:assembly-review-guidelines} for future reference.

\begin{aside}
\label{aside:assembly-review-guidelines}
\heading{Assembly Review Guidelines}

\textbf{TODO}: Move to reference appendix.

\end{aside}

First, let's review cross-sections along all major planes. Problems to look for in this step include:

- Component interference
- Component mis-alignment
- Incorrect fastener size

### Top Section Plane
\label{sec:assembly-review}

Take a \relation{Section-View}, select the desired section plane (in this case \relation{Top}), and use the triad \cadsymbol{Triad} to move the plane through the fasteners. Here, we notice a few things:

![\label{fig:fastener-cross-section-1} The hole, screw, and nut are all aligned.](images/figures/fastener-cross-section-1.png)

![\label{fig:screw-cross-section-void} There is an unexpected void in the screw. This is an artifact of how McMaster has created their screw and is inconsequential. This a good reminder that McMaster's CAD is imperfect\footnote{Most of the errors I find in McMaster parts are of little consequence. Errors are of greater consequence when 3-D printing parts, especially threaded features such as nuts and leadscrews. I re-model the threads yourself to avoid surprises, or to at least know who to blame.}. We will address this in the Exercises (Section~\ref{sec:exercises-bracket-assembly}).](images/figures/screw-cross-section-void.png)

![\label{fig:screw-thread-interference} There is interference between the threads on the screw and on the nut. This is only because they are not clocked for thread alignment. This is inconsequential.](images/figures/screw-thread-interference.png)

![\label{fig:screw-short} The screw is a bit short and doesn't engage all of the threads on the nut. As this threaded joint won't be full strength, we will address this shortcoming in the Exercises.](images/figures/screw-short.png)

![\label{screw-radial-clearance} Because our fastener (diameter 0.250") is smaller than our hole (diameter 0.256"), there is clearance between the two components (left image). Contrast this with the right image, where both components are the same diameter. If you design your parts as on the right, the fasteners will not slide through the holes.](images/figures/screw-radial-clearance.png)

### Right Section Plane

While we could sweep the top section plane up and down to review the assembly's other components, we'll get more information by taking other section planes. Take another section view along the \relation{Right} plane. 

![\label{fig:t-nuts-tangent} The two T-nuts on the vertical rail are tangent. Given the tolerances of the hole position within the nut, we may find that we cannot assemble the components because the nuts in fact interfere. In Section~\ref{sec:dimension-adjustments}, we will move these nuts farther apart.](images/figures/t-nuts-tangent.png)

![The vertical and horizontal rails do not interfere. You may say "of course they don't, because that's the way we mated them." It is so easy to screw up these small details, and the cost of checking is very low.](images/figures/rails-no-interference.png)

### Adjust the Part from the Assembly
\label{sec:dimension-adjustments}

From our reviews of the assembly cross-sections, we can confirm that the bracket accomplishes the goal set out at the start of Chapter~\ref{cha:tee-connector}. We will now address the problem that the T-nuts are contacting each other, as in Figure~\ref{fig:t-nuts-tangent}. 

While we could open the part file and edit the sketch, we can accomplish our goals without ever leaving the section view. If we double-click on a component feature, \solidworks{} displays the dimensions defining that feature, in this case the bracket extrude.

![](images/figures/bracket-dimensions-from-assembly.png)

Update the hole spacing from 1" to 1.5". Also increase the middle hole height to 0.75" away from the rail (instead of 0.5"). \relation{Rebuild} the part, and the bracket and assembly will update.

![](images/figures/bracket-updated-hole-spacing.png)

### Finishing Touches
\label{sec:finishing-touches}

Only when my part has stabilized do I add finishing touches to it. These include chamfers, fillets, engraved text and other (mostly) aesthetic considerations.

The opportunity that stands out on this part is to remove the sharp edges around the profile:
![](images/figures/bracket-sharp-edges.png)

Editing the bracket part directly, add a \relation{Fillet} and set the radius to 0.1"[^fillet-radius]. After selecting the first edge, a menu appears to assist in selecting other edges. In this case, *Connected to start loop* \cadsymbol{Connected-to-start-loop} will choose the other 5 edges.

[^fillet-radius]: Selecting fillet size involves a bit of guess-and-check unless dictated by other constraints. I change my increment size by a factor of three up or down (*i.e.* 1", 0.3", 0.1", 0.03" ...). \solidworks{} will fail to build fillets if they become large enough to remove the entire face, in which case I downsize until the part is happy again.

![](images/figures/bracket-assembly-finished.png)

This part and assembly is now complete, and both are of the quality where I would share them with others or send them out for manufacture.

## Exercises
\label{sec:exercises-bracket-assembly}

1. The bracket we've designed is strikingly similar to McMaster PN [47065T278](https://www.mcmaster.com/47065T278/), thus violating the adage "Don't make what you can buy." Download this part and take a look at how McMaster modeled it. What did we do better than McMaster? What did they do better than us?

2. The screw we originally used was (McMaster PN [90909A526](https://www.mcmaster.com/90909A526/)), but this screw is too short to engage all threads on the nut. Replace it with an appropriately long screw using the \relation{Replace-Components} tool. 

1. As mentioned in Section~\ref{sec:assembly-review}, both the original screw and the longer screw from the previous exercise has an unexpected void. Find where this void comes from and eliminate it. Doing so will create an error \cadsymbol{Error}. Use the four-step protocol in Section~\ref{sec:error-process} to resolve the error.

2. We used \kode{Copy with Mates}\cadsymbol{copy-with-mates} to create new fasteners in Section~\ref{sec:copy-with-mates}. This works for simple assemblies as the one here. However, it creates a duplicate of each copied component. In large assemblies, copying components will bog down the memory and make a messy feature tree. Use a \relation{Sketch-Driven-Pattern} to duplicate the screw and nut as follows:

2. The [moving sofa problem](https://en.wikipedia.org/wiki/Moving_sofa_problem) asks the following:
\begin{quote}
What is the largest area of a shape that can be maneuvered through a unit-width L-shaped corridor?
\end{quote}
Build a corridor of unit width and a [Hammersley sofa](https://en.wikipedia.org/wiki/Moving_sofa_problem#Lower) and confirm in an assembly that the sofa does in fact clear the corridor.