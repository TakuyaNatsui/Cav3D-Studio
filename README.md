# Cav3D Studio — 3D RF cavity and waveguide solver (trial edition)

[日本語の説明はこちら (Japanese)](README.ja.md)

Cav3D Studio is a Windows desktop application for designing RF cavities and waveguide components:
you build the geometry in a built-in 3D CAD, assign materials and boundary conditions, and compute
resonant modes, Q factors, S-parameters and fields in the same window.

The solver uses **second-order Nédélec (edge) elements on curved tetrahedra**, which gives high accuracy
with relatively few elements (for example, the TM010 mode of a pillbox cavity agrees with the analytic
frequency to within 0.1 % using about 1,300 elements).

This repository hosts the **releases (downloads), documentation and issue tracker** of Cav3D Studio.
It does not contain the source code of the application.

> **Trial edition:** all features are available, but an analysis can be run only on meshes with
> **up to 10,000 elements (tetrahedra)**. See [Trial limitations](#trial-limitations).

## Features

- **3D CAD**: sketches with geometric constraints and dimensions, extrude, revolve, boolean operations,
  fillets and chamfers, mirror, parameters; import of STEP / IGES / BREP files
- **Physics**: materials per region (εr, μr, dielectric loss tangent tanδ); boundary conditions
  PEC, electric wall (E-short), magnetic wall (M-short) for symmetry, and wave ports
- **Meshing**: curved second-order tetrahedral meshes with statistics and element quality
- **Eigenmode analysis**: resonant frequencies, fields (normalized to 1 J of stored energy),
  Q factor from wall loss (conductivity) and dielectric loss, geometry factor G, dissipated power
- **Port sweep (S-parameters)**: waveguide ports of arbitrary cross-section and coaxial (TEM) ports with
  characteristic impedance; S-parameters can be renormalized to a reference impedance (e.g. 50 Ω);
  adaptive frequency sweep; field snapshots at any frequency
- **Resonance search for one-port cavities** (e.g. couplers): resonant frequency f0, external Q (Qe),
  unloaded Q (Q0), loaded Q (QL) and coupling β
- **Visualization**: field arrows and colour maps on slices or on all elements, 2D slice view,
  fields and surface current on metal walls, S-parameter plots
- **Export**: CSV, VTK (ParaView), Touchstone (.sNp), field maps on a regular grid (HDF5 / CSV) for
  beam-dynamics codes; results are saved in HDF5 with the project
- **Command line**: the same executable runs analyses without the GUI (`Cav3D-Studio.exe --help`)
- User interface in Japanese and English

## System requirements

| | |
|---|---|
| OS | Windows 10 / 11, 64-bit |
| Memory | 8 GB or more recommended |
| Graphics | OpenGL 3.2 or later (used by the 3D view). Remote desktop sessions and some virtual machines may not provide it |
| Disk | about 2 GB (the extracted folder is about 1.7 GB) |

No installation or administrator rights are required.

## Download and start

1. Download `Cav3D-Studio-<version>-trial-win64.zip` from [Releases](https://github.com/TakuyaNatsui/Cav3D-Studio/releases).
2. (Optional) Check the file with the SHA-256 checksum in `SHA256SUMS.txt`:
   `certutil -hashfile Cav3D-Studio-<version>-trial-win64.zip SHA256`
3. Extract the zip to a local folder, for example `C:\Cav3D-Studio`.
   Folders synchronized by cloud storage (OneDrive, Dropbox, ...) are not recommended because the
   application consists of many files.
4. Run `Cav3D-Studio.exe` in the extracted folder.

The executable is **not code-signed** yet. Windows SmartScreen may show "Windows protected your PC";
click **More info** → **Run anyway** if you trust this download. Some antivirus programs may also flag
newly published executables; please report such cases in [Issues](https://github.com/TakuyaNatsui/Cav3D-Studio/issues).

To check the edition and the components found, run `Cav3D-Studio.exe version` in a terminal.

## Documentation

- [User manual (Japanese)](docs/USER_MANUAL.md) — installation, screen layout, three tutorials (a pillbox
  cavity, a cavity with beam pipes made by revolving a sketch, and a waveguide-coupled cavity with
  S-parameters and resonance search) and a reference of all functions. The same manual is included in the
  `docs` folder of the download.

## Trial limitations

- An analysis (eigenmode, port sweep, field snapshots, resonance search, and the command-line
  `run-cavity` / `run-driven`) can be run only on meshes with **at most 10,000 elements**.
  Larger meshes can still be generated and inspected; the analysis stops before solving with a message.
  Use a larger mesh size to reduce the number of elements.
- All other features (modelling, meshing, viewing and exporting results) are the same as the full edition.
- There is no restriction on the purpose of use: the trial edition may also be used commercially.
- Use of the trial edition is subject to the [Trial License Agreement](EULA.en.md)
  ([日本語（正本）](EULA.ja.md)).

## Licenses and source code of included components

- Cav3D Studio itself is proprietary software © 2026 Takuya Natsui, provided under the
  [Trial License Agreement](EULA.en.md).
- The application includes third-party open-source components (Qt / PySide6, VTK, Open CASCADE, NumPy,
  SciPy, Intel MKL and others). Their licenses and copyright notices are in `THIRD_PARTY_NOTICES.txt` in
  the application folder. Libraries under the LGPL are dynamically linked and can be replaced.
- The `mesher/` folder is a separate program distributed under the **GNU GPL v2 or later**. It contains
  Gmsh (https://gmsh.info) and the mesh-generation helper as source code. The source code of Gmsh is in
  `mesher/src/`, and the source code of the third-party libraries statically linked into the Gmsh DLL is
  provided as the release asset `Cav3D-Studio-<version>-mesher-sources.zip`
  (see the `README.txt` inside it, including a written offer under GPL v2 section 3(b)).

## Privacy

Cav3D Studio does not collect or send any usage data. Your models and results stay on your computer.

## Feedback

Bug reports, questions and requests are welcome in [Issues](https://github.com/TakuyaNatsui/Cav3D-Studio/issues). When reporting a problem,
please include the output of `Cav3D-Studio.exe version` and, if possible, the log shown in the
application. There is no guaranteed support for the trial edition.

---

© 2026 Takuya Natsui. All rights reserved (except third-party components, see above).
