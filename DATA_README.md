# F1–F9 trajectory and closed-loop time series

The `data` directory contains nine Excel workbooks, `F1.xlsx` through `F9.xlsx`,
one for each maneuver. Download a workbook from that directory, or use the
database ZIP linked in the repository README and open its `data` directory.

Each workbook provides the original geometry, sampled reference, nominal
closed-loop response and applied inputs in separate worksheets. The
motion-capture flight experiment reported in the paper is managed separately.

Open a workbook in a spreadsheet application or read the worksheets by name.
The first row is the column header; subsequent rows contain numeric data.
`ClosedLoop` and `Reference` have separate `time_s` columns at 0.01 s and 0.05 s
spacing. `OriginalGeometry` contains ordered spatial points. `ReadMe` provides
the case identifier and conventions.

`DATA_FORMAT.md` defines columns, coordinates, units and input timing.
`DATA_MANIFEST.json` lists workbook names, sizes and worksheet data-row counts.
