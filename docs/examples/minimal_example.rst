.. _minimal_example:

=================
A minimal example
=================

This page illustrates a minimal setup to get Thebe running, using
`mybinder <http://mybinder.org/>`_ as a
kernel (i.e. computation backend) provider. This guide will go step-by-step
in loading Thebe and activating it so that your code cells become active.

Loading and configuring Thebe
=============================

In order to use Thebe, we must first set its configuration. This must be
done **before** Thebe is loaded from a CDN or a local script.

Here's a sample configuration for Thebe

.. raw:: html

   <!-- Configure and load Thebe !-->
   <script type="text/x-thebe-config">
     {
       requestKernel: true,
       binderOptions: {
         repo: "binder-examples/requirements",
       },
     }
   </script>

.. code:: html

   <!-- Configure and load Thebe !-->
   <script type="text/x-thebe-config">
     {
       requestKernel: true,
       binderOptions: {
         repo: "binder-examples/requirements",
       },
     }
   </script>

In this case, ``requestKernel: true`` asks Thebe to request a kernel
immediately upon being loaded, and ``binderOptions`` provides the repository
that Binder will use to give us a Kernel.

Next, we'll load Thebe from a CDN:

.. raw:: html

   <script src="_static/thebe/index.js"></script>

.. code:: html

   <script src="https://unpkg.com/thebelab@latest/lib/index.js"></script>

Adding a button to activate Thebe
=================================

There are many ways you can activate Thebe. In this case, we'll add a
button to our page, and configure it to **bootstrap** Thebe once it is
clicked. We'll do this with a little bit of Javascript.

.. raw:: html

   <button id="activateButton" style="width: 150px; height: 75px; font-size: 1.5em;">Activate</button>
   <script>
   var bootstrapThebe = function() {
       thebelab.bootstrap();
   }

   document.querySelector("#activateButton").addEventListener('click', bootstrapThebe)
   </script>

Placing the button and adding the JavaScript to enable Thebe was done with the
code below:

.. code:: html

   <button id="activateButton"  style="width: 150px; height: 75px; font-size: 1.5em;">Activate</button>
   <script>
   var bootstrapThebe = function() {
       thebelab.bootstrap();
   }

   document.querySelector("#activateButton").addEventListener('click', bootstrapThebe)
   </script>


Adding code cells
=================

Finally, we'll add code cells that Thebe can activate. By default, Thebe
will look for any HTML elements with ``data-executable="true"``. We'll also add
a ``data-language="python"`` attribute to enable syntax highlighting with CodeMirror.


.. raw:: html

   <pre data-executable="true" data-language="python">print("Hello!")</pre>

Here's the code that created the cell above:

.. code:: html

   <pre data-executable="true" data-language="python">print("Hello!")</pre>

Press the Thebe button above to activate this cell, then press the "Run" button,
or "Shift-Enter" to execute this cell.

.. note::

   When Thebe is activated in this example, it must first ask Binder for a kernel.
   This may take several seconds.

Now let's try another cell that generates a Matplotlib plot. Because we've
configured Thebe to use Binder with an environment that has Numpy and
Matplotlib, this works as expected. Try modifying the cell contents and
re-running!

This is another cell, with plotting. Shift-Enter again!

.. raw:: html

   <pre data-executable="true" data-language="python">
   %matplotlib inline
   import numpy as np
   import matplotlib.pyplot as plt
   x = np.linspace(0,10)
   plt.plot(x, np.sin(x))
   plt.plot(x, np.cos(x))
   </pre>

Here's the HTML for the cell above:

.. code:: html

   <pre data-executable="true" data-language="python">
   %matplotlib inline
   import numpy as np
   import matplotlib.pyplot as plt
   x = np.linspace(0,10)
   plt.plot(x, np.sin(x))
   plt.plot(x, np.cos(x))
   </pre>
   
And here's an example where the contents cannot be modified once instantiated:

.. raw:: html

   <pre data-executable="true" data-language="python" data-readonly>print("My contents cannot be changed!")</pre>

For more examples, check out :ref:`more_examples`.
