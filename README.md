# Vector-thrust UAV maneuver database

Nine nominal closed-loop simulated maneuver records, F1–F9, for a dual-vector-thrust
flying-wing UAV. Each Excel workbook contains the original geometry, sampled
reference trajectory, closed-loop aircraft response and applied-control histories.

## Download

- [Download the database ZIP](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/archive/refs/heads/main.zip)
- [Browse the nine Excel workbooks](data)

Extract the ZIP and open the `data` directory to obtain `F1.xlsx` through `F9.xlsx`.
The repository contains one set of trajectory data and its documentation.

| Maneuver | Excel workbook |
|---|---|
| F1 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F1.xlsx) |
| F2 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F2.xlsx) |
| F3 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F3.xlsx) |
| F4 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F4.xlsx) |
| F5 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F5.xlsx) |
| F6 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F6.xlsx) |
| F7 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F7.xlsx) |
| F8 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F8.xlsx) |
| F9 | [Download](https://github.com/dynamics-pilot/vector-thrust-maneuver-data/raw/refs/heads/main/data/F9.xlsx) |

## Workbook contents

| Worksheet | Contents |
|---|---|
| `ClosedLoop` | Actual simulated state, kinematics, attitude, aerodynamic angles and applied inputs. |
| `Reference` | Sampled reference time, state, attitude and kinematics. |
| `OriginalGeometry` | Original ordered north, east and upward-height points. |
| `ReadMe` | Case identifier, declared maneuver end time, coordinates and timing conventions. |

The response and controls use 0.01 s spacing. Reference samples have a separate
0.05 s time vector. Units appear in the column headers. Full column definitions
and input timing are provided in [DATA_FORMAT.md](DATA_FORMAT.md).
[DATA_README.md](DATA_README.md) explains reading the workbooks;
[DATA_MANIFEST.json](DATA_MANIFEST.json) lists their sizes and row counts.

## License and citation

The dataset and its documentation are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
See [LICENSE](LICENSE) for the full terms. When reusing the data, cite its title
and repository address, and identify any changes you make.

Suggested reference: *Vector-thrust UAV maneuver database*, dynamics-pilot.
https://github.com/dynamics-pilot/vector-thrust-maneuver-data
