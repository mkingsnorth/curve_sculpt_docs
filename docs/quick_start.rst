.. _quick_start:

#################
Get Started
#################

Curve Sculpt 3D works through Blender's own *Curve* stroke method, so it is used from inside whichever
brush you are sculpting with. Once you have :ref:`installed<installation>` the add-on:

.. TODO: a GIF of these steps, start to finish.

#. Go into `Sculpt Mode <https://docs.blender.org/manual/en/latest/sculpt_paint/sculpting/index.html>`_ and pick a brush, for example *Draw* or *Crease*.

#. Open the brush's **Stroke** panel (in the tool settings along the top of the viewport, or in the sidebar's *Tool* tab) and click **Stroke Along 3D Curves**:

   .. image:: _static/images/stroke_panel_off.png
      :alt: Stroke Along 3D Curves

   This sets the brush's *Stroke Method* to *Curve* and turns on **Activate 3D Curves**.
   The same command is at the bottom of the *Sculpt* menu.

#. **Ctrl+right-click** on the mesh to place points (**Cmd+right-click** also works on a Mac).
   Each click adds a point to the end of the curve nearer the mouse. Hold **Ctrl** to see where the next point will go before you click.

#. Press **Enter** to run the brush along the curve, or **Ctrl+Enter** to run it inverted.

That's it. The curve stays on the mesh, so you can :ref:`edit it<drawing_curves>` and stroke it again, with the same brush or another.
**Ctrl+Z** undoes your last curve edit or stroke.

.. image:: _static/images/stroke_panel_on.png
   :alt: The Stroke panel with 3D curves on

With 3D curves on, the Stroke panel shows the settings for new points, the stroke's **Pressure** and :ref:`Taper<taper>`,
a :ref:`list of the mesh's curves<curve_list>`,
the **Draw Curve** button (and **−** beside it, to stroke inverted), a place to :ref:`import a curve object<importing_curves>`,
and **Shortcuts**, a cheat sheet of the :ref:`keys<keyboard_shortcuts>` that opens when you click it.

.. important::

    The *Stroke Method* belongs to each brush, so a brush set to *Curve* stays that way: dragging with it no longer
    sculpts freehand. Set its *Stroke Method* back to *Space* (or another method) to sculpt freehand again.
    Turning **Activate 3D Curves** off brings back Blender's own 2D paint curves for brushes on the *Curve* method.

.. tip::

    Your surface curves are saved with the mesh in the .blend file. They are only drawn while a brush on the
    *Curve* stroke method is in use with 3D curves on (and the viewport's overlays are shown), so they stay out of
    the way the rest of the time.
