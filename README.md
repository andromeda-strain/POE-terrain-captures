# POE-terrain-captures

The level-generator corpus of the POESniffer work tree (https://github.com/andromeda-strain/POESniffer),
mounted there as the submodule `captures/`. Split out of that repository on 2026-11-05 with its history
(`git filter-repo --subdirectory-filter captures`); every tool addresses it as `captures\...` relative to
the work tree, so nothing in the tools changed.

## Layout

- `<Area name> - <internal area id> - <seed>/` - one folder per captured load (the sniffer's capture driver
  creates it): the tracer's `stages_<stamp>.csv` (the draw log / the outdoor stage dumps), the client's
  truth grid, the simulator's `sim_<seed>*.tsv` exports, the walkability dumps and the renders.
- `cases/` - the corpus tables: `index.tsv` (one row per load: seed, area, generator, stages csv, truth
  grid, tile hash, verified, status, WorldAreas id - never reorder its columns, the tools index them by
  position), `sim_report.tsv` (the validator's verdict per load), the harvest tables the simulators read
  (`incursion_rooms.tsv`, `incursion_temple.tsv`, `lab_layouts.tsv`, `area_content.tsv`, ...) and
  `post_session.log`.
- `_unfiled/` - the September captures from before the capture driver filed them per area.
- `stages_<stamp>.csv` at the root - a tracer run the driver did not file (no index row).

## Working with it

Clone the parent with `git clone --recurse-submodules`, or `git submodule update --init` after the fact
(the corpus is about 9 GB checked out, 1.8 GB packed). New captures and regenerated sim exports are
committed here first, then the parent's submodule pointer is bumped.
