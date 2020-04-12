# AAE_Notebook_030_3D_Drone
This notebook is a continuation of the previous notebook AAE_Notebook_029_3dDrone.

## Tracking Rotation Rates

![Rotation Rates](/images/rotations.png)

We've seen how to go from rotor rotation rates to controls. We've seen how those controls can be thought of as a single, collective thrust and three differential thrusts which has torques/moments about the three rotation axes.

We've seen how to use the collective thrust, a rotation matrix, and two time integrals to advance the translational motion of the vehicle. Now, we're going to explore using the differential thrust to advance the rotational motion.

![Tracking Rotations](/images/tracking_rotations.png)

  1. Use the Euler's Equations to calculate the rotational acceleration of the vehicle in it's own body frame.
  2. Integrate that rotational acceleration to find the new p, q, r rotational velocities of the vehicle.
  3. Convert rotational velocities p, q, r (in the body frame) to a phi_dot, theta_dot, psi_dot (in the body frame).
  4. Integrate phi_dot, theta_dot, and psi_dot to get the final Euler angle orientations within the world frame.

** Note: Depending on which representation of attitude you use, the final step may look slightly different; however, at any rate, we need to translate body rotation rates into world frame attitude representations.

***   ***   ***   ***   ***   ***   ***   ***   ***

## Euler's Equations In A Rotating Frame

![Advancing Rotational Motion](/images/adv_rot_motions_eq.png)

We've seen the equation Mz = Iz(psi_dot_dot). This equation says that a moment (in this case, about the z axis) will cause a rotational acceleration about that axis. (With all of the variables being scalar numbers.)

In 3D, this equation changes. psi_dot_dot becomes omega_dot, a length 3 vector containing all three rotational accelerations. Mz becomes M, which is also a length three vector -- this vector giving moments about the x, y, and z axes. I becomes a 3 x 3 inertial matrix summarizing all moments of inertial.

Unfortunately, this is only valid whilst working in the world frame. 

![Euler's Rotation Equation](/images/eulers_equation.png)

When working in the body frame, we have the above [equation](https://en.wikipedia.org/wiki/Euler%27s_equations_(rigid_body_dynamics%29)) -- read "M is equal to I times omega_dot plus omega cross with I omega", wherein we're taking the cross-product.

As we saw previously, omega is just a vector of the body rates: omega = [pqr]. Thus, omega_dot = [p_dot, q_dot, r_dot].

The [cross product](https://en.wikipedia.org/wiki/Cross_product) within the equation is just a way of multiplying two vectors. In example, if you have two vectors, a and b, with an angle theta between them, the cross product is given by a x b = c, where c is a vector that's perpendicular to both a and b. The direction of c is given by the right-hand rule and the magnitude (size) is given by the equation |c| = |a| |b| sin(theta)
