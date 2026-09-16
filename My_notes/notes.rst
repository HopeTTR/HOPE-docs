My practice notes
=================

.. toctree::
   :maxdepth: 2

   MHD
   appendix
   stellar_Oscillation

Suppose a magnetized star satisfies the MHD force-balance equation,

.. math::

   \boxed{
   -\nabla P
   - \rho \nabla \Phi
   + \frac{1}{\mu_0}
   (\nabla \times \mathbf{B}) \times \mathbf{B}
   = 0
   }

The pressure-gradient force, gravity, and Lorentz force exactly balance one
another. Therefore, the net force on the fluid is zero and the fluid initially
has no acceleration.

We therefore call this configuration an **equilibrium**.

“long-term stability” Check?
----------------------------

If established magnetic configuration inside a star produces restoring forces if we introduce a tiny plasma displacement, that oppose the displacement, then the configuration is stable. Otherwise, it is unstable.
For stellar magnetic instabilities, this growth can occur on roughly an Alfvén timescale, which can be extremely short compared with the evolutionary lifetime of the star.
So if a magnetic structure disrupts itself after only a few \(t_A\), it is not a credible explanation for a magnetic field supposed to survive for millions or billions of years.

The importance of how centrally concentrated the magnetic energy is has been found to affect both stellar magnetic equilibria and their eventual topology.
At fixed \(B_0\), reducing \(r_0,B)\ means more centrally concentrated makes the strong-field region smaller. 


Problems:
~~~~~~~~~

Even after taking all physical checks before submitting the run, the simulation can still fail due to numerical issues. For example, the simulation can fail due to a sudden drop in hydro time step. This can be caused by various factors such as numerical instabilities, boundary conditions, or physical processes that are not well-resolved in the simulation.
Under the space where most check variables are in good range first numerical error we got is due to the sudden drop in hydro time step. As we know the hydro time step is calculated based on the CFL condition, which depends on the local sound speed and grid resolution. If the sound speed becomes very small or the grid resolution becomes very high, the hydro time step can become very small, leading to numerical instability and simulation failure.
formula of :ref:`CFL Condition <cfl-condition>` is given by

.. math::

   \Delta t = \frac{C_{\text{CFL}}}{\max(c_s, v_A)} \min(\Delta x, \Delta y, \Delta z)

where :math:`C_{\text{CFL}}` is the Courant number, :math:`c_s` is the sound speed, :math:`v_A` is the Alfvén speed, and :math:`\Delta x`, :math:`\Delta y`, :math:`\Delta z` are the grid spacings in each direction.

The WD interior is not causing the tiny timestep; the combination of non-zero magnetic field and the low-density (fluff) outer region is causing the tiny timestep. FLASH uses a global explicit CFL timestep based on MHD characteristic speeds, which means that the smallest timestep in the entire simulation domain determines the timestep for the entire simulation.

For example, for run_38,

.. math::

   \left(\frac{v_A}{c}\right)_{\mathrm{bulk}} = 0.0654,

which is fine for the conservative Newtonian criterion we selected, whereas

.. math::

   \left(\frac{v_A}{c}\right)_{\mathrm{box}} = 6.75

occurs at exactly

.. math::

   \rho = 5 \times 10^{-5} \; \mathrm{g\,cm^{-3}}

near :math:`r \simeq R_{\mathrm{WD}}`. Since :math:`v_A = B / \sqrt{4\pi\rho}`, this is precisely the expected low-density-atmosphere problem.

So if we fixed the magnetic field and current density (old) is :math:`B_0` and :math:`J_0`, the Alfvén speed would be :math:`v_{A,0} = B_0 / \sqrt{4\pi\rho_0}`.

.. list-table:: Required fluff density for different Alfvén-speed limits
   :header-rows: 1
   :widths: 40 60
   :align: center

   * - Target whole-domain :math:`v_A/c`
     - Required :math:`\rho_{\rm fluff}`

   * - 1.0
     - :math:`2.28 \times 10^{-3}\ {\rm g\,cm^{-3}}`

   * - 0.5
     - :math:`9.1 \times 10^{-3}\ {\rm g\,cm^{-3}}`

   * - 0.3
     - :math:`2.53 \times 10^{-2}\ {\rm g\,cm^{-3}}`

   * - 0.1
     - :math:`2.28 \times 10^{-1}\ {\rm g\,cm^{-3}}`

But putting very high density in the fluff region is not a good idea, because it will affect several serious physical and numerical artifacts. So we can reduce the magnetic field strength to reduce the Alfvén speed in the low-density region. This can be done by reducing the magnetic field strength in the initial conditions or by using a magnetic field that is more centrally concentrated, which will reduce the magnetic field strength in the low-density region.

The fluff is simply a numerical replacement for vacuum outside the star; ideally it should interact as little as possible with the WD.

And it will have non-negligible :math:`P_{\rm fluff} = B^2/(8\pi)`. A mismatch between the WD surface pressure and fluff pressure can launch pressure waves.
