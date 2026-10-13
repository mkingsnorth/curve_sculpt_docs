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
Hidden curves are left out. All the curves go into a single stroke, so a single **Ctrl+Z** undoes it; the brush is not dragged
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

A few brushes only work with particular mesh settings, and Blender normally hides them otherwise. Curve Stroke tells you why
rather than run them without:

* *Erase Multires Displacement* and *Smear Multires Displacement* need a Multires modifier.
* *Simplify* needs Dynamic Topology.

----------------------------------------------------------------------

---------------------------------
Size and Pressure
---------------------------------

The brush's own **Size** decides the stroke's width. With the size set in pixels (the default) it is measured at the depth of each
point on the curve, so the stroke keeps the width the brush shows on screen there; with the *Radius Unit* set to *Scene* it is the same
everywhere.

Each dab's pressure is the **Pressure** setting in the Stroke panel times the curve's :ref:`point pressure<point_pressure>` at that spot.
Pressure only changes the stroke if the brush uses pressure for its strength or size.

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

Curves work on meshes sculpted with a Multires modifier, with some limits, because Blender only lets add-ons see a Multires mesh's
*unsculpted* surface while sculpting:

* Along the parts of a curve you can **see**, each dab is placed on the real, sculpted surface by Blender itself.
* Along parts **out of view** (behind the mesh), dabs follow the unsculpted surface, so heavily sculpted areas there may not be followed exactly.
  Turn the view so the curve is visible for the best result.
* A curve that runs out of view is stroked in two parts, which Blender records as two undo steps; **Ctrl+Z** undoes both together.
* Points are placed on the unsculpted surface, so on a large sculpted form they may appear to sit inside it.
  The curve is still drawn, and strokes along it still land on the sculpted surface where it can be seen.

.. note::

    Meshes using Dynamic Topology haven't been tested as thoroughly yet. If curves seem not to follow your latest sculpting,
    please :ref:`let us know<contact>`.
