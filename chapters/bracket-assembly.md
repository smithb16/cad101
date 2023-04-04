# Bracket Assembly

In this chapter, we'll take the bracket (Chapter~\ref{cha:tee-connector}), two segments of extrusion, and some fasteners and build them into a digital assembly. This will help tell us with greater certainty whether our design has accomplished our goals.

## A New Assembly

After creating a new assembly, we are met with the "Insert Parts" dialog box. Since we're planning to insert multiple parts, pin \cadsymbol{Pin} the dialog. Insert the tee connector (PT-XXX-Bracket) by selecting it from the menu, then clicking in the design space.

![](images/figures/first-assembly-insert-part)

Repeat the insertion process with two extrusions (McMaster PN [47065T503](https://www.mcmaster.com/47065T503-47065T1/)). Using the download process from Section~\ref{sec:define-constraints}, download a screw (McMaster PN [XXX](tbd)) and extrusion nut (McMaster PN [XXX](tbd)). Add both to the assembly. 

With the parts populated, we will use mates to define their orientation in the assembly. As constraints are to a 2D sketch, mates are to a 3D assembly. In the parts tree, with one exception, all parts have the prefix "(-)", meaning they are not fully constrained and can be moved around. The first part we dropped into the assembly has the prefix "f", meaning it is fixed in space. This is unfortunate because it is fixed in a random location, potentially far from the assembly's origin. Right-click on this fixed part and select \kode{Float}.

## Adding Mates

Ourt next task is to constrain the assembly. First, let's choose one part and fully constrain it in our assembly. This part will then act as the foundation for all other parts. The foundation part should be a part that:

1. Doesn't move with resspect to the assembly (*i.e.* no rotating or translating)
2. Serves a prominent role in the assembly

Let's choose the plate (PRT-002 from Chapter~\ref{cha:tee-connector}) as our foundation part. Using the \relation{Mate} tool, add a *Coincident* relation between the part origin and the assembly origin, as in Figure~\ref{fig:bracket-assembly-origin}. 

With this one mate, our part is fully constrained. The "(-)" prefix has disappeared. We cannot drag the part around. Note that this mate is now in our part tree in two locations, once under the part and once under the list of assembly mates. The mate also has the Ground symbol \cadsymbol{ground}, meaning it contributes to grounding this part.

![\label{fig:bracket-assembly-origin}](images/figures/bracket-assembly-origin.png)

### Position the Rails

Next, mate the horizontal rail. I prefer to mate parts when they're in roughly the correct orientation, rather than floating randomly in space. Use the \relation{Triad} tool to move the rail near the plate, as in Figure~\ref{fig:bracket-assembly-triad}. With the rail oriented, it is easier to see which planes and faces we should mate together to constrain he rail. 

![\label{fig:bracket-assembly-triad}](images/figures/bracket-assembly-triad.png)

\questiontriangle Which mate(s) are needed to constrain the horizontal rail?

Unfortunately, constraining origins won't give the results we're after. All mates should be \mate{Coincident}:

\begin{center}
\begin{tabular}{ccc}
  & \textbf{Bracket} & \textbf{Extrusion} \\
  \hline
  \mate{Coincident} & \emph{Main Face} & \emph{Main Face} \\
  \mate{Coincident} & \emph{Edge Face} & \emph{Other Main Face} \\
  \mate{Coincident} & \emph{Right Plane} & \emph{Right Plane} \\
  \hline
\end{tabular}
\end{center}

Repeat the same process with the second, vertical rail to arrive at Figure~\ref{fig:bracket-assembly-rails-oriented}. At this point, we can confirm (or deny) that the bracket achieved the goal of orienting the rails as intended.

![\label{fig:bracket-assembly-rails-oriented}](images/figures/bracket-assembly-rails-oriented.png)

## Adding One Fastener

While the big pieces of the assembly are now in place, it is incomplete until we put the fasteners in. All of the fasteners[^all-fasteners]. I'm opinionated on this matter because I've burned myself too many times. Here's a few reasons I populate all fasteners in my models:

1. If your fasteners don't fit and you have to hand-modify hardware, that can easily double your assembly time.
2. If you populate fasteners, \solidworks can automatically generate an accurate Bill of Materials (BOM).
3. Assessing tool access to each fastener is challenging unless the fastener is present. Our minds are not good at filling in the missing parts.

[^all-fasteners]: One of my CAD review guidelines is "Your assembly isn't complete until it has all of the fasteners." For my full review guideline, see Box~\ref{aside:review-guidelines}.

With philosophy out of the way, let's take action. First, let's get the screw in place with these mates:

\begin{center}
\begin{tabular}{ccc}
  & \textbf{Bracket} & \textbf{Fastener} \\
  \hline
  \mate{Concentric} & \emph{Hole} & \emph{Any round face or edge} \\
  \mate{Coincident} & \emph{Main face} & \emph{Underside of head} \\
  \hline
\end{tabular}
\end{center}

Repeat the same steps to locate the T-nut on the fastener. I'll let you decide which mates are needed. While there is no sense in constraining the screw in rotation, we should constrain the nut rotation, perhaps with a \mate{Parallel} mate. Otherwise, it may poke through the extrusion rail.

## More Fasteners

Now that we've specified one fastener set, we can easily get more. Select both the nut and screw. *Right-click* on one and \kode{Copy with Mates}. By copying both parts at once, they are duplicated as a set. 

![\label{fig:copy-with-mates}](images/figures/copy-with-mates.png)

For any mates that we want to re-use exactly (as in our coincident mates), check the "Repeat" box. For others, such as the concentric and parallel mates, select the hole or face that we want to use instead. Doing so will create a new fastener set, and the dialog will remain open to create more sets until we close it.

With the fasteners installed, our assembly is complete. Congratulations! We will take time in the exercises breaking, fixing, and modifying it. However, because of the way we've designed and assembled the plate, we will never have to rebuild the parts from ground zero. 

\begin{aside}
\label{aside:review-guidelines}
\heading{Assembly Review Guidelines}

test

\end{aside}