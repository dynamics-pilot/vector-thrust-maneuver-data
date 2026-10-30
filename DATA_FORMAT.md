# Excel data format and units

Each trajectory is supplied as one `.xlsx` workbook, `F1.xlsx` through `F9.xlsx`.
Cells contain numeric values and text; the workbooks have no macros or formulas.
Numeric time series use SI units. Display formatting is separate from the stored values.

## Worksheets

| Worksheet | Records |
|---|---|
| `ClosedLoop` | Complete nominal closed-loop response and applied inputs, one sample per row at 0.01 s spacing. |
| `Reference` | Sampled reference state and kinematics, one sample per row at 0.05 s spacing. |
| `OriginalGeometry` | Ordered original path points, without an imposed time vector. |
| `ReadMe` | Case identifier, declared maneuver end time, coordinates, timing conventions and license. |

The first row contains column names. Units are included in the names: `m`, `mps`,
`mps2`, `rad`, `radps`, `radps2` and `per_s` denote metres, metres per second,
metres per second squared, radians, radians per second, radians per second
squared and inverse seconds. Normalized rotor speeds, quaternion components,
rotation matrices, flags and load factor are dimensionless.

## Coordinates and attitude

Inertial vectors use north–east–down (NED). `height_m` is upward height, equal to
`-p_D_m`. Body vector components use the instantaneous aircraft axes.
The Hamilton quaternion `[q_w,q_x,q_y,q_z]` is scalar-first and represents the
active body-to-NED rotation. `R_BN_ij` is matrix element `(i,j)`, with inertial
row `i` and body-axis column `j`. Euler angles use the ZYX display convention.

Total inertial acceleration and its body-axis representation are recorded
separately from the derivative of body-velocity components, which includes
the rotating-frame contribution. Specific force is total inertial acceleration
minus gravitational acceleration.

## Closed-loop columns

The `ClosedLoop` worksheet has 70 columns.

| Quantity | Columns |
|---|---|
| Time (s) | `time_s` |
| Position in NED (m) | `p_N_m`, `p_E_m`, `p_D_m` |
| Upward height (m) | `height_m` |
| Velocity in NED (m/s) | `v_N_mps`, `v_E_mps`, `v_D_mps` |
| Velocity in body axes (m/s) | `v_b_x_mps`, `v_b_y_mps`, `v_b_z_mps` |
| Total inertial acceleration in NED (m/s²) | `a_N_mps2`, `a_E_mps2`, `a_D_mps2` |
| Total inertial acceleration expressed in body axes (m/s²) | `a_b_x_mps2`, `a_b_y_mps2`, `a_b_z_mps2` |
| Time derivative of body-velocity components (m/s²) | `dv_b_dt_x_mps2`, `dv_b_dt_y_mps2`, `dv_b_dt_z_mps2` |
| Scalar-first attitude quaternion | `q_w`, `q_x`, `q_y`, `q_z` |
| Quaternion time derivative (1/s) | `dq_w_dt_per_s`, `dq_x_dt_per_s`, `dq_y_dt_per_s`, `dq_z_dt_per_s` |
| Body-to-NED rotation matrix, listed by row | `R_BN_11`, `R_BN_12`, `R_BN_13`, `R_BN_21`, `R_BN_22`, `R_BN_23`, `R_BN_31`, `R_BN_32`, `R_BN_33` |
| ZYX display roll, pitch and yaw (rad) | `roll_rad`, `pitch_rad`, `yaw_rad` |
| Angular velocity in body axes (rad/s) | `omega_b_x_radps`, `omega_b_y_radps`, `omega_b_z_radps` |
| Angular velocity in NED (rad/s) | `omega_N_radps`, `omega_E_radps`, `omega_D_radps` |
| Angular acceleration in body axes (rad/s²) | `domega_b_dt_x_radps2`, `domega_b_dt_y_radps2`, `domega_b_dt_z_radps2` |
| Angular acceleration in NED (rad/s²) | `domega_dt_N_radps2`, `domega_dt_E_radps2`, `domega_dt_D_radps2` |
| Speed (m/s) | `speed_mps` |
| Specific-force magnitude divided by gravitational acceleration | `load_factor` |
| Specific force in NED (m/s²) | `specific_force_N_mps2`, `specific_force_E_mps2`, `specific_force_D_mps2` |
| Specific force in body axes (m/s²) | `specific_force_b_x_mps2`, `specific_force_b_y_mps2`, `specific_force_b_z_mps2` |
| Horizontal course (rad) | `course_rad` |
| Upward-positive flight-path angle (rad) | `flight_path_angle_rad` |
| Applied vectoring angles (rad) and dimensionless normalized rotor speeds | `tilt_1_rad`, `tilt_2_rad`, `rotor_1_normalized`, `rotor_2_normalized` |
| Declared-maneuver indicator (0/1) | `within_declared_maneuver` |
| Saved terminal-extension indicator (0/1) | `is_terminal_extension` |
| Angle of attack (rad) | `aoa_rad` |
| Sideslip angle (rad) | `sideslip_rad` |

The state order is position, scalar-first quaternion, inertial velocity and body
angular velocity: `p_N_m,p_E_m,p_D_m,q_w,q_x,q_y,q_z,v_N_mps,v_E_mps,v_D_mps,
omega_b_x_radps,omega_b_y_radps,omega_b_z_radps`.
State derivatives use inertial velocity, quaternion derivatives, inertial
acceleration and body angular acceleration in that order. Shared components
are stored once in the flat table. The height column supplies the upward
coordinate used in the trajectory figures.

## Reference columns

The `Reference` worksheet has 30 columns. It contains `time_s`, NED position,
NED velocity and acceleration, the scalar-first quaternion, the nine
`R_BN_ij` elements, body angular velocity and angular acceleration, and
`is_terminal_extension`. Names and units follow `ClosedLoop`.
Its time vector is independent of the response time vector; row numbers
need not coincide between the two worksheets.

## Original geometry

`OriginalGeometry` contains `point_index,p_N_m,p_E_m,height_m`.
The index gives the original traversal order. These spatial points have
no assigned time law.

## Applied-input timing

The two tilt angles and normalized rotor-speed columns at `time_s(i)` give
the input applied until the next response sample. The final row repeats
the last applied input to accompany the terminal state. Acceleration and
derivative records at an input change use the newly applied input;
the final derivative records use the last input. The declared maneuver and
its saved terminal extension are retained and identified by their 0/1 flags.
The declared end time is recorded in `ReadMe`.
