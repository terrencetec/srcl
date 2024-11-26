# srcl

## Dependencies

conda
- cmake
- spdlog
- pybind11
- pyyaml

conda-forge
- python-foton

pypi
- cdsutils

git clone
- [rtsfreerun](https://git.ligo.org/christopher.wipf/rtsfreerun.git)

## Signal flow

SRCL control signal goes to SR2 and SRM via the LSC matrix.
However, SRM has zero gains in DRIVEALIGN, meaning SRCL signal only goes through SR2.

SRCL is the input of M3_LOCK.
Output of M3_LOCK is the input of M2_LOCK and the actuation signal of M3.
Output of M2_LOCK is the input of M1_LOCK and the actuation signal of M2.
Output of M1_LOCK actuates M1.

![control_definition](control_definition.png)

The control diagram explains how the CTRL and PLANT blocks are populated.

## Filter configurations:

**SRCL**

FM 1, 2, 3, 4, 7, 9, 10

Gain = 0.4

Plant from M3 -> M3: FM 5

**M1_LOCK**

FM 1

Gain = 1

Plant from M1 -> M2: FM 10

**M2_LOCK**

FM 1, 2, 3, 4, 5, 9

Gain = 1.3

Plant from M2 -> M3: FM 10

**M3_LOCK**

FM None

Gain = 1

Plant in SRCL module.

Gain in DRIVEALIGN L2L = 1.5.


## Repository

`/data` contains 2 dtt .xml files.
One contains an open loop transfer function measurement of SRCL.
Another contains a spectrums of the SRCL_IN1 and SRCL_IN2.

`/foton_files` contains the L1LSC.txt and L1SUSSR2.txt filter files.

`srcl_oltf.ipynb` reconstructs the open loop transfer function from the
filters and the suspension plant models, which also exist in the filter files.
