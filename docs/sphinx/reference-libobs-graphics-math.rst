Extra Math Functions/Macros
===========================

Helper functions/macros for graphics math.

.. macro:: #define RAD(val) ((val)*0.0174532925199432957692369076848f)

   Macro that converts a floating point degrees value to radians.

.. macro:: #define DEG(val) ((val)*57.295779513082320876798154814105f)

   Macro that converts a floating point radians value to degrees.

.. macro:: #define LARGE_EPSILON   1e-2f

   Large epsilon value.

.. macro:: #define EPSILON         1e-4f

   Epsilon value.

.. macro:: #define TINY_EPSILON    1e-5f

   Tiny Epsilon value.

.. macro:: #define M_INFINITE      3.4e38f

   Infinite value

---------------------

.. function:: float rand_float(int positive_only)

   Generates a random floating point value (from -1.0f..1.0f, or
   0.0f..1.0f if *positive_only* is set).
