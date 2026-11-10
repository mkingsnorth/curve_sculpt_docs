.. _stroking:

#####################################
Stroking Along Curves
#####################################

---------------------------------
Running a Stroke
---------------------------------

Press **Enter** (or click **Draw Curve** in the Stroke panel) to run the brush along the curves.
**Ctrl+Enter** (or the **−** button beside Draw Curve) runs it inverted, as holding Ctrl does while sculpting.

The stroke runs along every **ticked** curve in the :ref:`curve list<curve_list>`, or along the active curve if none are ticked.
Ticked curves are stroked even while hidden, so you can hide them to see the result. All the curves go into a single stroke, so a single **Ctrl+Z** undoes it; the brush is not dragged
across the gaps between them.

Commands for stroking are also in the *Sculpt* menu while 3D curves are on: *Draw Curve*, *Draw Curve Inverted* and *Import Curve Object*.

----------------------------------------------------------------------

---------------------------------
Brushes
---------------------------------

Any sculpt brush can be used, including **Mask**, **Face Set** and colour **Paint** brushes: the stroke runs inside the brush's
own tool, exactly as a hand-drawn stroke would. The brush's settings in the header (size, strength, direction, falloff, texture)
all apply.

Each of Blender's built-in sculpt brushes has been checked against Blender's own 2D curve stroke along the same path, and nearly
all give the same result. A few behave differently, or not at all, along a curve:

* **Boundary** brushes, the **Grab Cloth** brushes, **Grab Silhouette** and **Scene Project** do nothing along a curve, as with Blender's own 2D curves.
* **Twist** turns the surface by the angle the stroke sweeps around its start, so it is very sensitive to the curve's exact shape.
* The cloth-simulated **Pose** brushes (*Bend/Twist Cloth*, *Stretch/Move Cloth*) move the mesh further than Blender's 2D curve does.

A few brushes only work with particular mesh settings, and Blender normally hides them otherwise. Curve Sculpt 3D tells you why
rather than run them without:

* *Erase Multires Displacement* and *Smear Multires Displacement* need a Multires modifier.
* *Simplify* needs Dynamic Topology.

----------------------------------------------------------------------

---------------------------------
Size and Pressure
---------------------------------

The brush's own **Size** decides the stroke's width. With its *Size Unit* set to *View* (pixels, the default) it is measured at the depth
of each point on the curve, so the stroke keeps the width the brush shows on screen there; set to *Scene*, it is the same everywhere.
A size in pixels covers less of the mesh on a high-resolution screen, so a 4K monitor may need a much bigger number for the same result: set
*Size Unit* to *Scene* if you want a stroke to come out the same on any screen.

A stroke always uses the active brush and its current settings: curves don't remember a brush, so the same curve can be stroked with any brush, one after another.

Each dab's pressure is the **Pressure** setting in the Stroke panel times the curve's :ref:`point pressure<point_pressure>` at that spot,
times the :ref:`taper<taper>` there.
:ref:`Pressure Affects<taper_affects>` decides what that pressure changes: the stroke's size, its strength, or both. You don't need a pen for any of this.

----------------------------------------------------------------------

.. _brush_direction:

---------------------------------
Which Way the Brush Pushes
---------------------------------

A stroke pushes the way the same brush does by hand. Use the brush's own direction (the **+** and **−** in the tool header) to choose whether it
adds or carves, or **Ctrl+Enter** to run it the other way for one stroke. Which way counts as "out" comes from the brush's settings, such as
*Sculpt Plane* in its Brush Settings panel, which curve strokes follow too.

----------------------------------------------------------------------

.. _taper:

---------------------------------
Taper
---------------------------------

**Taper Start** and **Taper End** in the Stroke panel taper every curve's ends without setting point pressures:
the pressure rises over the first part of each curve and falls over the last, easing in and out, from and to the **Fade To** value below them.
Each is a share of the curve's length, so 0.25 tapers the first (or last) quarter, whatever the curve's size; 0 leaves that end as it is.

The taper multiplies the point pressures, so the two work together: taper the ends automatically, and shape the middle with **Alt+S**.
The rings around the points shrink or fade with it, so you can see the taper before stroking.
Start and end follow the curve's direction, which the arrow near its end shows; :ref:`switch_direction` reverses it.

**Fade To** is the pressure the taper fades to at the tips. At 0, the default, they fade to nothing, so even a small taper thins the very end of a stroke, and because dabs overlap,
the effect reaches about a brush radius in from the end. A higher value leaves the tips part-way, for a softer taper.

On a :ref:`closed curve<closed_curves>` the taper fades in and out at its first point, the seam.

.. _taper_affects:

Pressure Affects
================

**Pressure Affects**, under Pressure, sets what pressure changes along a curve: the **Pressure** setting, each point's own pressure (**Alt+S**) and the taper.
While you press **Alt+S**, the header says what it will change:

* **Size and Strength** (the default): the stroke gets thinner and lighter towards a tapered end, like a brush lifted off the page.
* **Size**: the stroke narrows to a point. With brushes such as *Draw*, whose depth follows their size, it gets shallower too,
  as it would with a pen, but less than with Size and Strength.
* **Strength**: the stroke keeps its width and fades out.
* **Brush Settings**: the brush's own pen-pressure toggles (the pen icons beside its *Size* and *Strength*)
  decide. With both off, pressure and taper don't change the stroke at all.

The first three ignore the brush's pen icons, so no pen settings are needed, and leave them as they were: the add-on sets them only for the length
of the stroke, so the brush isn't marked as changed. Where the dabs get smaller they get closer together too, as they do in a hand stroke,
so a fine tip stays smooth instead of beading.

----------------------------------------------------------------------

.. _curves_meet:

---------------------------------
Where Curves Meet
---------------------------------

Where curves stroked together meet, at a branch or a crossing, their strokes add up, so the meeting point comes out
higher (or deeper) than the curves either side of it. Testers found the first two of these give the cleanest joins:

* **Point pressure.** Select the point where a branch starts and set its pressure to zero with **Alt+S**
  (see :ref:`point pressure<point_pressure>`). The branch then fades in from nothing where it meets the curve, instead of
  adding a lump.
* **The Layer brush.** *Layer* raises the surface to a set height and never builds up within a stroke, so curves stroked
  together with it join without a bump.
* **Blend Overlaps** (below), which does much the same as the first automatically.

.. _blend_overlaps:

Blend Overlaps
==============

**Blend Overlaps** in the Stroke panel (off by default) eases each curve off where the curves before it have already
been, so overlapping curves read more like one stroke.

* The curves are blended in the order they are listed: the first is stroked as it is, and the later ones fade where
  they meet it and come back to full strength about a brush radius further on.
* It eases the brush's strength, not its size, whatever :ref:`Pressure Affects<taper_affects>` is set to, so a branch keeps
  its width as it fades into the curve before it, and the taper and point pressure go on setting the size.
* In testing, a *Draw* branch's junction came out no higher than the curve it joins, and a *Draw Sharp* one a couple of
  percent higher. Leave it off with *Layer*, which never builds up anyway: with it on, a junction comes out a couple of
  percent higher.
* It only applies within one stroke. Stroking the same curves again adds on top, as a second hand stroke would.

----------------------------------------------------------------------

.. _stroke_settings:

---------------------------------
Stroke Settings
---------------------------------

The brush's *Stroke* panel settings apply to curve strokes as they do to hand-drawn ones:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Setting
     - In a curve stroke
   * - **Spacing**
     - The gap between dabs, as a share of the brush size.
   * - **Spacing Distance**
     - *View* measures the gaps on screen, *Scene* over the surface. Where a curve runs round the side of a form, *View*
       spacing is kept from spreading the dabs so far apart that they no longer overlap.
   * - **Adjust Strength for Spacing**
     - Strength is scaled to the spacing, so the stroke has the same depth whatever the spacing.
       Curve strokes were checked against hand-drawn strokes and match their depth to within a few percent.
   * - **Dash Ratio** / **Dash Length**
     - Gaps are left in the stroke, as in a hand-drawn one.
   * - **Jitter**
     - Dabs are moved at random across the surface, by the same amount a hand-drawn stroke's would be, including the
       *Jitter Unit* and pen pressure options.
   * - **Input Samples**
     - Doesn't apply: it smooths the mouse, and a curve stroke has none.

----------------------------------------------------------------------

.. _multires:

---------------------------------
Multires
---------------------------------

Curves work on meshes sculpted with a Multires modifier. Blender only lets add-ons see a Multires mesh's *unsculpted* surface
while sculpting, so:

* When you stroke, Curve Sculpt 3D first reads the real, sculpted surface and places every dab on it, so the stroke follows your
  sculpting, in view or not, just as on a mesh without Multires. On a big mesh this takes a moment (about a second at two
  million faces), and the cursor shows it's busy.
* Points are placed on the unsculpted surface, so on a large sculpted form they may appear to sit inside it.
  The curve is still drawn, and strokes along it still land on the sculpted surface.

.. note::

    With Dynamic Topology on, Curve Sculpt 3D catches up with your latest sculpting each time you place points or stroke,
    which takes a moment on a very large mesh. If curves still seem not to follow your sculpting, please :ref:`let us know<contact>`.
