# 🌊 NEMO3.6 Directory Structure

This document describes the architecture of the NEMO3.6 OGCM framework and explains the purpose of the major directories used for noCC / CC experiments.

---

# 🗂️ Root Directory Structure

<details>
<summary><strong>Click to expand root directory tree</strong></summary>

```text
../
├── ARCH
├── CONFIG
├── EXTERNAL
├── fcm-make
├── NEMO
├── SETTE
├── TOOLS
└── License_CeCILL.txt
```
</details>

---

# 📂 Main Directories

| Directory | Description | Editable |
|---|---|---|
| `ARCH/` | HPC and compiler configuration | ✅ |
| `CONFIG/` | Experiment configuration | ✅ |
| `EXTERNAL/` | External libraries and dependencies | ⚠️ |
| `fcm-make/` | Build and compilation system | ⚠️ |
| `NEMO/` | Original NEMO source code | ❌ |
| `SETTE/` | Testing framework | ⚠️ |
| `TOOLS/` | Utility scripts and preprocessing tools | ✅ |

---

> [!WARNING]
> The original `NEMO/` source code should NEVER be modified directly.

---

# ⚙️ Simulation Workflow

```mermaid
graph LR

A[Modify Configuration]
--> B[Compile nemo.exe]
--> C[Submit HPC Job]
--> D[Generate Outputs]
--> E[Post-processing]
```

---

# 🧪 Experiment Configuration

Example experiment:

```text
CONFIG/ORCA1_PISCES_FLX/
```

This directory contains all files required for the PISCES flux-based experiments.

---

## 📁 `ORCA1_PISCES_FLX/` Structure

<details>
<summary><strong>Click to expand experiment directory</strong></summary>

```text
ORCA1_PISCES_FLX/
├── MY_SRC
├── BLD
├── PARAM
└── SCRIPTS
```

</details>

---

### 🔧 `MY_SRC/`

Contains user-modified Fortran (.f90) source code.

Typical usage:
- parameter tuning
- customized physical schemes
- experimental model development

> [!IMPORTANT]
> Files inside `MY_SRC/` override the original NEMO source files during compilation.

> [!WARNING]
> The original `MY_SRC/` source code should NOT be modified.


---

### 🏗️ `BLD/`

Compiled executable file: 
```text
BLD/bin/nemo.exe
```

Used to launch simulations on HPC systems.

---

### ⚙️ `PARAM/`

Contains runtime configuration files.

```text
PARAM/
├── NAMELIST
└── XML
```
---

#### 📝 `NAMELIST/` Configuration

<details>
<summary><strong>Click to expand namelist structure</strong></summary>

```text
PARAM/NAMELIST/
├── namelist_ref
└── namelist_pisces_cfg
```

</details>

---

##### 📄 `namelist_ref`

Default reference namelist provided by NEMO.

> [!WARNING]
> This file should NOT be modified directly.

---

##### 📄 `namelist_pisces_cfg`

User-defined experiment configuration.

Typical modifications include:
- simulation length
- timestep settings
- restart configuration
- biogeochemical parameters

---

#### 📤 `XML/` Output Configuration

<details>
<summary><strong>Click to expand XML structure</strong></summary>

```text
PARAM/XML/
├── file_def_nemo-opa.xml
└── field_def_nemo-opa.xml
```

</details>

---

##### 📄 `file_def_nemo-opa.xml`

Controls:
- output frequency
- output files
- temporal averaging

Examples:
- monthly outputs
- yearly outputs

---

##### 📄 `field_def_nemo-opa.xml`

Defines model output variables.

Examples:
- temperature
- salinity
- ocean currents
- biogeochemical tracers

---

### 📜 `SCRIPTS/`

Contains job execution and submission scripts.

Typical usage:
- HPC batch submission
- simulation automation
- workflow management

---

# 🌊 NEMO Source Code Structure

Contains original Fortran (.f90) source code.

<details>
<summary><strong>Click to expand source code structure</strong></summary>

```text
NEMO/
└── OPA_SRC/
    ├── SBC
    ├── LBC
    ├── TRA
    └── ZDF
```

</details>

---

## 🧩 Core Physical Modules

| Module | Description |
|---|---|
| `SBC/` | Surface boundary conditions |
| `LBC/` | Lateral boundary conditions |
| `TRA/` | Tracer equations (e.g., temperature and salinity) |
| `ZDF/` | Vertical mixing and diffusion schemes |

---

## 🌬️ `SBC/` — Surface Boundary Conditions

Examples:
- air-sea heat flux
- freshwater flux
- wind stress

---

## 🌊 `LBC/' — Lateral Boundary Conditions

Used for:
- open ocean boundaries
- regional configurations

---

## 🌡️ `TRA/` — Tracer Processes

Handles:
- temperature
- salinity
- passive tracers
- biogeochemical tracers

---

## 🌪️ `ZDF/` — Vertical Mixing

Controls:
- turbulent mixing
- vertical diffusion
- stratification parameterizations

---

# 📌 Best Practices

✅ Modify:
- `namelist_pisces_cfg`
- `MY_SRC/`
- `XML/` output files `file_opa` or `field_opa`
- job scripts
  
❌ Avoid modifying:
- original `NEMO/` source files
- `namelist_ref`

---

# 📚 Related Documentation

- `workflow.md`
- `compilation.md`
- `experiments.md`
- `namelist.md`
- `xml_output.md`
