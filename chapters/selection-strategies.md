# Selection Strategies

\begin{aside}
\label{aside:selection-strategies}
\heading{Selection Strategies}

In CAD, try as we might, we can't get around use of the cursor and mouse for selection. Here's some strategies to reduce our clicking:

* Within the Feature Tree or Assembly Tree, as with both Windows and MacOS, we can select multiple items by holding the \texttt{Ctrl} or \texttt{Cmd} key while we select. We can also hold \texttt{Shift} while selecting within a list to highlight all items between the clicks.

![](images/figures/multi-select.png)

* Within the design pane, we can select multiple items by dragging a window across the pane. Dragging up-and-left creates an XX window, which selects all items touched by the window. Dragging up-and-right creates an XX window, which selects all items enclosed by the window.

![](images/figures/window-drags.png)

If you would like to select all of a certain part within an assembly, you can filter it with the Assembly Tree filter.

![](images/figures/assembly-tree-filter.png)

We can use \cadsymbol{selection-filters}\kode{Selection Filters} to select only the entities we want. This feature is found within the Selection Filter toolbar. I use the \cadsymbol{select-edges}\kode{Select Edges} filter when filleting to avoid selecting faces. I use the \cadsymbol{select-faces}\kode{Select Faces} filter when isolating parts within an assembly (Section~\ref{sec:isolating-parts}). Beyond that, I leave the Selection Filters alone.

![](images/figures/selection-filters-toolbar.png)

\end{aside}