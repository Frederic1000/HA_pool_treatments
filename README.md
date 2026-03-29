# Pool Water Analysis — Home Assistant Package

Self-contained HA package for pool water analysis, treatment recommendations and treatment logging.

## Features
- Manual entry of pH, free chlorine, temperature
- Configurable pool volume
- Configurable product ratios (g per unit per m³)
- Automatic dosing recommendations for pH+, pH-, shock chlorine, slow chlorine
- Treatment logging via `custom:multiple-logbook-card` with auto-reset after save
- History graph for pH and chlorine

## Prerequisites

Install the following custom card via HACS before setting up the dashboard:
- **multiple-logbook-card** by Royto (HACS > Frontend)

## Installation

### 1. Enable packages in configuration.yaml
Add these lines if not already present:
```yaml
homeassistant:
  packages: !include_dir_named packages
```

### 2. Copy the package file
```
config/
└── packages/
    └── pool/
        └── pool.yaml
```

### 3. Restart Home Assistant
All entities (input_number, sensors, automation) are created automatically.

### 4. Add the Pool view to your main dashboard

The pool view is designed to be added as a new tab in your existing main dashboard,
not as a separate dedicated dashboard.

Steps:
1. Go to your main dashboard
2. Click **⋮ (top right) > Edit dashboard**
3. Click the **"+" icon** next to the existing view tabs to add a new view
4. In the view settings, switch to **YAML mode**
5. Replace the content with the contents of `lovelace_pool.yaml`
6. Save — a new "Pool" tab (🏊 icon) appears in your main dashboard

## Product ratio defaults
| Product        | Default | Meaning                                  |
|----------------|---------|------------------------------------------|
| Slow chlorine  | 16 g/m³ | 16 g raises chlorine by 1 mg/L in 1 m³  |
| Shock chlorine | 10 g/m³ | 10 g raises chlorine by 1 mg/L in 1 m³  |
| pH+ granules   | 15 g/m³ | 15 g raises pH by 0.1 in 1 m³           |
| pH- granules   | 15 g/m³ | 15 g lowers pH by 0.1 in 1 m³           |

Adjust ratios directly in the dashboard (Product ratios card) to match your specific products.

## Target ranges
| Parameter     | Min    | Max      |
|---------------|--------|----------|
| pH            | 7.0    | 7.6      |
| Free chlorine | 1.0 mg/L | 3.0 mg/L |

## Default pool volume
Set to **40 m³** — adjust in the dashboard (Product ratios card > Volume) or
directly in `pool.yaml` under `pool_volume > initial`.
