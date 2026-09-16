Appendix
========

.. _dipole-field-derivation:

Dipole Magnetic Field Derivation
--------------------------------

Full calculation goes here.

.. _alfven-speed-derivation:

Alfven Speed Derivation
-----------------------

Full calculation goes here.

Mass-Radius Relation for white dwarfs
-------------------------------------
Unlike normal stars, white dwarfs have inverse mass-radius relation: as mass increases, radius decreases. This is because white dwarfs are supported by electron degeneracy pressure, which behaves differently than thermal pressure in normal stars.

.. _cfl-condition:

CFL Condition
-------------
During one timestep, informationshould not move faster than the numerical methode can properly track on the grid. This is known as the Courant-Friedrichs-Lewy (CFL) condition, which is a stability condition for numerical simulations. The CFL condition states that the time step must be small enough such that the distance information can travel in one time step is less than the grid spacing. Mathematically, it can be expressed as:

.. math::

   \Delta t = \frac{C_{\text{CFL}}}{fastest signal speed} \min(\Delta x)

where :math:`C_{\text{CFL}}` is the Courant number, fastest speed means :math:`c_s+|v|_max` :math:`c_s` is the sound speed, and |v|_max is the maximum velocity, in mhd it will be :math:`v_A` the Alfvén speed, and :math:`\Delta x`is the grid spacings in each direction.

