#####################################
Tips and Troubleshooting
#####################################

==========================
Frequently Asked Questions
==========================

.. note::

    If you are having any issues do not hesitate to :ref:`Contact Us <contact>`

----------------------------------------------------------------------------------
Ctrl+right-click doesn't add a point. Why?
----------------------------------------------------------------------------------

Check that:

* You are in Sculpt Mode, with a mesh as the active object.
* The brush's *Stroke Method* is *Curve* and **Activate 3D Curves** is on in its Stroke panel.
  The quickest way is the **Stroke Along 3D Curves** button, shown while the brush is on another stroke method (see :ref:`quick_start`).
* You are clicking on the mesh: points can only be placed on its surface.
* You aren't clicking right on an existing point or handle: there, Ctrl+right-click pulls out that point's handles instead.
* The active curve isn't hidden. If it is, Ctrl+right-click starts a new curve instead.

----------------------------------------------------------------------------------
Where have my curves gone?
----------------------------------------------------------------------------------

Curves are only drawn while a brush on the *Curve* stroke method is in use with 3D curves on, so picking a brush on another stroke method
hides them. They are still on the mesh. They also follow the viewport's **Show Overlays** toggle, and hidden curves
(the eye in the :ref:`curve list<curve_list>`) aren't drawn at all.

----------------------------------------------------------------------------------
Draw Curve is greyed out. Why?
----------------------------------------------------------------------------------

There is nothing to stroke: the mesh has no curves yet. Ctrl+right-click on the mesh to start one.

----------------------------------------------------------------------------------
I press Enter and nothing (or hardly anything) happens. Why?
----------------------------------------------------------------------------------

Most often the mesh has too few vertices for the brush. A sculpt brush can only move the mesh's own vertices, so on a
low-poly mesh (Blender's Suzanne has 500 faces) a small brush lands mostly between them and next to nothing moves.
Curve Sculpt 3D warns in the status bar when a stroke hardly changed the mesh. To fix it:

* Add detail to sculpt: a **Multires** modifier (subdivide it a few times), **Remesh**, or Dynamic Topology.
* Or make the brush bigger, so it reaches the vertices.

.. note::

    A **Subdivision Surface** modifier makes a low-poly mesh *look* smooth and detailed, but adds no vertices to
    sculpt: strokes still move the low-poly mesh underneath, and the smooth surface you see sits inside it, so curves
    can appear to float above the surface. Use Multires instead, or apply the Subdivision Surface modifier first.

----------------------------------------------------------------------------------
The stroke is weaker than I expected.
----------------------------------------------------------------------------------

The brush's **Adjust Strength for Spacing** setting (on by default) lowers its strength so that overlapping dabs add up to about
one dab's depth. Hand-drawn strokes do the same; turn the setting off in the brush's Stroke panel for a deeper stroke, or raise the brush's strength.
Also check the **Pressure** setting in the Stroke panel and the curve's :ref:`point pressure<point_pressure>`.

----------------------------------------------------------------------------------
I set point pressure but the stroke doesn't taper.
----------------------------------------------------------------------------------

Check :ref:`Pressure Affects<taper_affects>` in the Stroke panel. With it set to *Brush Settings*, pressure only changes a stroke if the brush
uses it: turn on pressure for the brush's *Strength* or *Size* (the pen icons beside them), or choose one of the other options.

----------------------------------------------------------------------------------
Alt+S changes both size and strength, even with only the Size pen icon on.
----------------------------------------------------------------------------------

The pen icons only count when :ref:`Pressure Affects<taper_affects>` is on *Brush Settings*. Otherwise Pressure Affects decides, and the header says what Alt+S will change.
With brushes such as *Draw*, whose depth follows their size, **Size** alone also makes the stroke shallower, as it would with a pen.

----------------------------------------------------------------------------------
Sharp brushes bead on stretches running away from me.
----------------------------------------------------------------------------------

From a very glancing view, a stretch of curve running away from you is short on screen, and with *Spacing Distance* on *View* the dabs on it can end up far apart. Stroke from a less glancing view, or set the brush's *Spacing Distance* to *Scene*.

----------------------------------------------------------------------------------
The stroke cuts under a raised form between two points.
----------------------------------------------------------------------------------

Between two points, the line and the stroke take the short way, and may pass under a form that stands well above them, such as an ear. Add a point on top of the form so the curve goes over it.

----------------------------------------------------------------------------------
G, R and S don't do what they usually do in Sculpt Mode.
----------------------------------------------------------------------------------

Blender's Curve stroke method uses G, R and S to move, rotate and scale its curve points, so while a brush is on it they don't pick the Grab or Smooth brush, or
set the voxel size. Use the toolbar or the asset shelf for those, or set the brush back to another stroke method.

.. _moving_points_view:

----------------------------------------------------------------------------------
Points jump when I orbit part way through a move.
----------------------------------------------------------------------------------

G, R and S work from the screen: each selected point follows the mouse, then finds the surface under it from the current view. If an orbit takes a point round the edge of the form,
the surface under it from there is on the front, so that's where it lands. Orbit first and then start the move, or keep the selected points in view while you orbit. **Esc** or a right-click puts everything back.

----------------------------------------------------------------------------------
A curve has come away from the surface. How do I put it back?
----------------------------------------------------------------------------------

This can happen after reshaping the mesh. Moving points makes them find the surface again from the current view. Choose a view that shows the curve, select its points with **A**, press **G**, move the mouse a little and left-click to confirm.

----------------------------------------------------------------------------------
The paint curve drop-down in the Stroke panel keeps going back to empty.
----------------------------------------------------------------------------------

That is Blender's own 2D paint curve, which isn't used while 3D curves are on, so it is kept empty to avoid confusion.
Your 2D paint curves are kept in the file: turn **Activate 3D Curves** off to use them again.

The *Draw Curve* button beside it is Blender's too, and has nothing to stroke while 3D curves are on. To stroke your 3D curves,
use the **Draw Curve** button below the curve list, or press **Enter**.

----------------------------------------------------------------------------------
Ctrl+Z undid a curve edit rather than my stroke.
----------------------------------------------------------------------------------

Ctrl+Z steps back through curve edits and strokes together, newest first, so an edit made after a stroke is undone before the stroke.
Settings changed between curve edits are the exception: those are undone after the curve edits around them.
See :ref:`undo`.

----------------------------------------------------------------------------------
Does it work with Multires?
----------------------------------------------------------------------------------

Yes. Strokes follow the sculpted surface; on a big mesh each stroke takes a moment to start. See :ref:`multires`.

----------------------------------------------------------------------------------
"Getting the surface ready…" appears and Blender pauses. Why?
----------------------------------------------------------------------------------

Curve Sculpt 3D keeps its own copy of the mesh's surface for placing points, and rebuilds it after you sculpt.
On a large mesh (over about 200,000 faces) that takes a moment, so the note is shown while it happens, the first time you
place or move a point after a stroke. Moving points without sculpting in between doesn't need it again.
