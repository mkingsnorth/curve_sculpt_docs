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
  The quickest way is the **Stroke Along 3D Curves** button (see :ref:`quick_start`).
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

There is nothing to stroke: the mesh has no curves yet, or the ticked curves are all hidden. Hover over the button to see which.

----------------------------------------------------------------------------------
The stroke is weaker than I expected.
----------------------------------------------------------------------------------

The brush's **Adjust Strength for Spacing** setting (on by default) lowers its strength so that overlapping dabs add up to about
one dab's depth. Hand-drawn strokes do the same; turn the setting off in the brush's Stroke panel for a deeper stroke, or raise the brush's strength.
Also check the **Pressure** setting in the Stroke panel and the curve's :ref:`point pressure<point_pressure>`.

----------------------------------------------------------------------------------
I set point pressure but the stroke doesn't taper.
----------------------------------------------------------------------------------

Pressure only changes a stroke if the brush uses it. Turn on pressure for the brush's *Strength* or *Size* (the pen icons beside them).

----------------------------------------------------------------------------------
The paint curve drop-down in the Stroke panel keeps going back to empty.
----------------------------------------------------------------------------------

That is Blender's own 2D paint curve, which isn't used while 3D curves are on, so it is kept empty to avoid confusion.
Your 2D paint curves are kept in the file: turn **Activate 3D Curves** off to use them again.

----------------------------------------------------------------------------------
Ctrl+Z undid a curve edit rather than my stroke.
----------------------------------------------------------------------------------

Ctrl+Z steps back through curve edits and strokes together, newest first, so an edit made after a stroke is undone before the stroke.
See :ref:`undo`.

----------------------------------------------------------------------------------
Does it work with Multires?
----------------------------------------------------------------------------------

Yes, with some limits on parts of a curve that are out of view. See :ref:`multires`.

----------------------------------------------------------------------------------
"Getting the surface ready…" appears and Blender pauses. Why?
----------------------------------------------------------------------------------

Curve Stroke keeps its own copy of the mesh's surface for placing points, and rebuilds it after you sculpt.
On a large mesh (over about 200,000 faces) that takes a moment, so the note is shown while it happens, the first time you
place or move a point after a stroke. Moving points without sculpting in between doesn't need it again.
