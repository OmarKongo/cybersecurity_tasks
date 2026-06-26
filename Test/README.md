# Chapter 5 — Seismic Forces on Buildings: The General Procedure, the SFRS, the ELF Method, and Load Combinations

## Overview

Chapter 5 is the heart of the course — where everything from Chapters 1–4 converges into the actual **seismic force calculation** for a building. Chapters 1–3 built the physics (seismology, earthquake characteristics, vibration theory); Chapter 4 introduced the codes, the Risk Category / importance factor, the ground-motion parameters, and the Seismic Design Category. Chapter 5 now uses all of it to (1) build the **design response spectrum**, (2) characterize the **seismic force-resisting system (SFRS)**, and (3) compute and distribute the **seismic forces** by the Equivalent Lateral Force (ELF) procedure, then combine them with the other loads.

The chapter is long and proceeds in a deliberate order:

- **The general procedure for the design response spectrum (Steps 1–6)** — Site Class → mapped $S_S$/$S_1$ → site coefficients $F_a$/$F_v$ → adjusted $S_{MS}$/$S_{M1}$ → design $S_{DS}$/$S_{D1}$ → the four-segment spectrum — and **when the site-specific procedure becomes mandatory**.
- **The fundamental period** $T$ (four methods) and the **Seismic Design Category (SDC)** determination.
- **The SFRS** — the six system categories of ASCE 7 Table 12.2-1, the system/height limitations, and the three response characteristics **$R$, $\Omega_0$, $C_d$**; combining systems.
- **Structural irregularities** (horizontal and vertical) and the limitations they trigger.
- **The Equivalent Lateral Force (ELF) procedure** — base shear $V = C_s W$, vertical distribution $F_x$, story shear $V_x$, overturning moment $OTM_x$, **story drift**, the **P-Delta effect**, building separation, orthogonal interaction, and the ELF permitted/not-permitted limits.
- **The simplified alternative procedure** (§12.14).
- **Reducing the base shear** (inelastic damage, base isolation, damping systems).
- **Seismic load effects** ($E$, the redundancy factor $\rho$, the overstrength load $E_m$) and the **load combinations** (LRFD / ASD / overstrength).

The destination throughout is the **internal seismic force on each element**, ready to be combined with gravity and other loads for design.

---

## Prerequisites from earlier chapters

Chapter 5 is the most dependency-heavy chapter in the course — it pulls forward concepts from all four earlier chapters (per the validated dependency graph). Review these before reading the detailed notes:

**From Chapter 1 (seismology):**
- **Body waves — P and S waves** *(Ch 1, P01, ⏱ 00:39:23, p. 1-8)* — the shear (S) wave is why **shear-wave velocity** is the primary measure of Site Class in Step 1.

**From Chapter 2 (earthquake characteristics):**
- **Uniform-risk / probability of collapse** *(Ch 2, P02, ⏱ 00:20:45, p. 2-10)* — the **1%-in-50-years** target that the general procedure's risk-targeted basis is built on.
- **Building period $T \approx 0.1N$** *(Ch 2, P03, ⏱ 00:06:23, p. 2-12)* — reappears as **Method 2** for the approximate period of moment frames.
- **Catastrophic resonance — Mexico City 1985** *(Ch 2, P03, ⏱ 00:24:23, p. 2-13)* — the cautionary case for **when base isolation is detrimental** (soft soil, long-period site).

**From Chapter 3 (vibration theory):**
- **Stiffness / combining members (parallel & series)** *(Ch 3, P01, ⏱ 00:07:36, p. 3-2)* — needed for elastic story drift and the soft/weak-story irregularities.
- **Natural period of an SDOF system** *(Ch 3, P01, ⏱ 00:24:17, p. 3-3)* — the period that every period-estimation method approximates.
- **Damping & the damping ratio ($\beta$ = 5%)** *(Ch 3, P01, ⏱ 00:33:20, p. 3-5)* — the spectrum's damping assumption and the basis of hysteretic behavior.
- **MDOF — degrees of freedom & modes** *(Ch 3, P01, ⏱ 00:42:42, p. 3-7)* and **fundamental vs. higher modes / modal mass participation** *(Ch 3, P01, ⏱ 00:51:19, p. 3-8)* — the lumped-mass model for $W$ and the exponent $k$ in the vertical distribution.
- **Spectral values $S_a$, $S_v$, $S_d$** *(Ch 3, P02, ⏱ 00:00:02, p. 3-9)*, the **response spectrum & smoothing** *(Ch 3, P02, ⏱ 00:15:49, p. 3-9)*, and the **effect of damping** *(Ch 3, P02, ⏱ 00:21:27, p. 3-11)* — the three zones (constant acceleration / velocity / displacement) of the design spectrum.
- **Base shear $V = m\,S_a = C_s W$** *(Ch 3, P02, ⏱ 00:36:50, p. 3-12)* — the equation the whole ELF procedure expands.

**From Chapter 4 (codes & ground motion):**
- **Seismic design philosophy — accept damage, prevent collapse** *(Ch 4, P01, ⏱ 00:26:00, p. 4-7)* — the basis of $R$ and the hysteretic (inelastic) approach.
- **Risk Category & importance factor $I_e$** *(Ch 4, P02, ⏱ 00:06:34, p. 4-9 and ⏱ 00:38:53, p. 4-11)* — feed the SDC and the drift limits.
- **The MCE chain** — risk-targeted $\text{MCE}_R$ *(Ch 4, P03, ⏱ 00:03:45, p. 4-12)*, **Site Class A–F** *(⏱ 00:07:53, p. 4-13)*, **mapped $S_S$/$S_1$** *(⏱ 00:14:44, p. 4-14)*, **adjusted/design accelerations** *(⏱ 00:23:25, p. 4-14)*, and the **design PGA & four-segment spectrum / the 2/3 factor** *(⏱ 00:33:02, p. 4-15)* — Chapter 5 now executes this chain step by step.
- **Seismic Design Category — what it affects & the six SDCs** *(Ch 4, P04, ⏱ 00:00:02, p. 4-16 and ⏱ 00:03:41, p. 4-17)*.
- **Permitted design methods & the two limit states** *(Ch 4, P04, ⏱ 00:29:11, p. 4-19)* — the basis of the LRFD/ASD load combinations.
- **Structural analysis & the load path (SFRS)** *(Ch 4, P04, ⏱ 00:34:16, p. 4-19)* — the load path this chapter designs.

---

## Detailed notes

### The SFRS — horizontal (diaphragms) and vertical elements

Lateral forces on a building are resisted by a combination of horizontal and vertical elements, collectively the **seismic force-resisting system (SFRS)** (*the load path from Ch 4*).[[cite n="1" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="00:01:41" page="5-2"]]

**Horizontal elements — the diaphragms** (the floors you stand on):
- **Flexible diaphragms** (e.g., wood light-frame construction).
- **Rigid diaphragms** (concrete slabs).
- **Horizontal trusses** (e.g., roof trusses over a large retail store).

**Vertical elements** (Figure 5.1):
- **Shear walls.**
- **Braced steel frames:**
  - **Concentrically Braced Frame (CBF)** — the diagonal meets the beam-column connection, or the diagonals meet one another.
  - **Buckling-Restrained Braced Frame (BRBF)** — a casing engulfs the diagonal to restrain it from buckling; a form of CBF.
  - **Eccentrically Braced Frame (EBF)** — the diagonal meets only the beam (not the beam-column connection and not another diagonal), creating a **link**.
- **Moment-Resisting Frame (MRF)** — rigid (moment) connections between beams and columns that can resist moment.
- **Dual system** — a combination of a moment-resisting frame with a braced steel frame, or with shear walls (e.g., MRF bays on the sides and a braced frame or shear wall in the middle bay).

Vertical elements vary by **material** (shear walls: concrete, wood, masonry, or steel-plate; moment frames: concrete or steel) and by the **level of seismic detailing** of their connections:
- **Special** — stringent detailing to ensure energy dissipation at the connection.
- **Intermediate** — in between.
- **Ordinary** — no special seismic detailing.

The combination of vertical and horizontal elements gives the complete SFRS that resists lateral seismic forces.

### The design response spectrum — general versus site-specific procedure

The design response spectrum is based on the **risk-targeted $\text{MCE}_R$** (*from Ch 4*). Two procedures are available:[[cite n="2" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="00:22:04" page="5-3"]]

1. **General procedure** — the main method for the exam; based on the **uniform-risk methodology** (the seismologists' hazard maps combined with the engineers' fragility curves through the risk integral to meet the **1%-in-50-years** target probability of collapse, *from Ch 2*). Used for typical buildings and soils.
2. **Site-specific procedure** — required when the general procedure **cannot** be used. It accounts for regional seismicity and geology, magnitude, return period, and fault location; the engineer develops the ground motion (site response analysis or ground motion hazard analysis). This is above exam level — but you **must** know **when** the general procedure cannot be used and the site-specific procedure becomes mandatory.

The general procedure has **six main steps** to construct the design response spectrum.

### Step 1 — Site Class: how it is determined and classes A–E

Select the **Site Class (A–F)** from ASCE 7 Table 20.3-1, reproduced as **Table 5.1**.[[cite n="3" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="00:26:39" page="5-4"]] Site Class is based on the **average soil properties in the top 100 ft** below the original ground, using **shear-wave velocity** (*the S-wave from Ch 1*), **standard penetration resistance** (SPT $N$, blows per foot, not to exceed 100 — and $N_{ch}$ for cohesionless/sand layers only), and **undrained shear strength** $s_u$ (cohesive/clay layers). Criteria:

| Site Class | Description | Criteria (any one) |
|---|---|---|
| **A** | hard rock | shear-wave velocity > 5,000 ft/s |
| **B** | rock | shear-wave velocity 2,500–5,000 ft/s |
| **C** | soft rock / very dense soil | velocity 1,200–2,500 ft/s, **or** SPT $N$ > 50 blows/ft, **or** $s_u$ > 2,000 psf |
| **D** | stiff soil | velocity 600–1,200 ft/s, **or** SPT $N$ 15–50, **or** $s_u$ 1,000–2,000 psf |
| **E** | soft clay / bay mud | velocity < 600 ft/s, **or** SPT $N$ < 15, **or** $s_u$ < 1,000 psf; **or** a soil profile with a layer > 10 ft thick having PI > 20, moisture content ≥ 40%, **and** $s_u$ < 500 psf |

### Step 1 — Site Class F (problematic soils) and choosing the softer class

**Site Class F — problematic soils** (cannot use the general procedure; require the site-specific **site response analysis**). Site Class F where **any** of the following is satisfied:[[cite n="4" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="00:36:32" page="5-4"]]

1. Soils vulnerable to potential failure or collapse under seismic loading: **liquefiable** soils, **quick and highly sensitive clays**, **collapsible weakly cemented** soils.
2. **Peat and/or highly organic clay** with a layer thickness > 10 ft.
3. **Very high plasticity clay** with a layer thickness > 25 ft and PI > 75.
4. **Very thick soft-to-medium stiff clay** with a layer thickness > 120 ft and $s_u$ < 1,000 psf.

A common exam question gives several soil descriptions and asks which **cannot** use the general procedure — the answer is the **Site Class F** soil.

**When two criteria give different classes, assign the SOFTER soil — the higher letter.** Worked example: shear-wave velocity 1,300 ft/s → Site Class C (1,200–2,500); average SPT $N = 49$ → Site Class D (15–50). Choose the higher letter → **Site Class D**.

### Averaging soil properties over layers and the default site class

When the top 100 ft has several layers, **average over only the top 100 ft** (ASCE 7 Eqs 20.4-1 to 20.4-4):[[cite n="5" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="00:41:13" page="5-5"]]

- **Average shear-wave velocity:** $\bar{v}_s = \dfrac{100}{\sum (d_i / v_{si})}$, where $d_i$ is the thickness of layer $i$ and $v_{si}$ its shear-wave velocity.
- **Average SPT:** $\bar{N} = \dfrac{100}{\sum (d_i / N_i)}$.
- **Cohesionless (sand) layers only:** $N_{ch} = \dfrac{d_s}{\sum (d_i / N_i)}$, where $d_s$ = total thickness of the cohesionless layers in the top 100 ft.
- **Cohesive (clay) layers only:** $\bar{s}_u = \dfrac{d_c}{\sum (d_i / s_{ui})}$, where $d_c$ = total thickness of the cohesive layers in the top 100 ft.

**Default site class:** when the geotechnical report is not available, select **Site Class D** as the default (IBC 1613.2.2, ASCE 7 20.1) — unless the building official or geotechnical data determines that Site Class E or F is likely present. **For the exam, if no soil information is given, assume Site Class D.**

### Step 2 — mapped spectral accelerations $S_S$ and $S_1$

From the code maps determine:[[cite n="6" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="01:02:05" page="5-6"]]
- **$S_S$** — mapped spectral response acceleration at the **short period (0.2 s)**.
- **$S_1$** — mapped spectral response acceleration at the **long period (1 s)**.

Sources: IBC Figures 1613.2.1 through .8, or **ASCE 7 Figures 22-1 through 22-8**. Only the California-relevant figures are in the handout: **Figure 22-1** gives $S_S$ and **Figure 22-2** gives $S_1$.

**Assumptions in the maps:** (1) **5% critical damping** (*the $\beta$ = 5% value from Ch 3* — a fair assumption, little effect); (2) the site has a shear-wave velocity of **2,500 ft/s** — i.e., the building is on **rock** (the B/C borderline). This rock assumption must later be **corrected for the actual soil**.

**Reading the maps:** find the intersection of the building's latitude and longitude and read the contour value (a multiple of 100); divide by 100 → a fraction of $g$. Example: at 40° N, 120° W the contour reads 150 → 150/100 = 1.5 → $S_S = 1.50\,g$. An exam question requiring you to read these maps is unlikely unless an enlarged snippet is provided (the contours are too clustered to read by eye).

### Step 3 — site coefficients $F_a$ and $F_v$

From **Table 5.2** (ASCE 7 Tables 11.4-1 and 11.4-2):[[cite n="7" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="01:11:17" page="5-6"]]
- **$F_a$** — acceleration site coefficient, a function of the **Site Class** and the short-period mapped acceleration $S_S$.
- **$F_v$** — velocity site coefficient, a function of the **Site Class** and the 1-second mapped acceleration $S_1$.

Worked readings: Site Class C, $S_S = 0.5$ → $F_a = 1.3$. Site Class C, $S_1 = 0.62$ → $F_v = 1.4$ (the 0.6 column region).

### Site coefficient superscript notes and linear interpolation

**Table 5.2 superscript notes** (apply mainly to Site Classes D and E):[[cite n="8" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="01:16:54" page="5-7"]]

- **Superscript a** (Site Class D, $F_a$): use the listed values when Site Class D was determined from **measured** soil properties. If D was the **default** site (no measured properties), $F_a$ shall **not be less than 1.2**.
- **Superscript b** (Site Class D, $F_v$): you may use the listed values **provided** the seismic response coefficient $C_s$ is calculated conservatively by injecting the **1.5 factor** at the four indicated locations in the $C_s$ equations. Effectively this **modifies the design response spectrum**: extend the constant-acceleration plateau from $T_S$ out to $1.5\,T_S$, and increase both descending branches by **50%** (×1.5). Otherwise, develop a site-specific ground motion hazard analysis.
- **Superscript c** (Site Class E, $F_a$): the table shows "…" (no value) — as a conservative alternative use $F_a$ equal to that of Site Class C (1.2); otherwise develop a site-specific analysis.
- **Superscript d** (Site Class E, $F_v$): no value given — $F_v$ is **not required** when the structure's period $T \le T_S$ **and** the ELF (static) procedure is used. If $T > T_S$, a site-specific ground motion hazard analysis is required.

**Linear interpolation** for intermediate $S_S$ or $S_1$ values: identify the bracketing columns (left = col 1, right = col 2), read $S_S$ and $F_a$ from each, then:

$$F_a = F_{a,\text{col2}} + \frac{S_{S,\text{col2}} - S_S}{S_{S,\text{col2}} - S_{S,\text{col1}}} \times \left( F_{a,\text{col1}} - F_{a,\text{col2}} \right)$$

### Steps 4 & 5 — adjusted ($S_{MS}$, $S_{M1}$) and design ($S_{DS}$, $S_{D1}$) accelerations

**Step 4 — Adjusted (modified) accelerations:** correct the mapped (rock) values for the actual soil:[[cite n="9" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="01:46:59" page="5-7"]]

$$S_{MS} = F_a \times S_S \qquad\qquad S_{M1} = F_v \times S_1$$

**Step 5 — Design accelerations:** factor the adjusted values down by **two-thirds**:

$$S_{DS} = \tfrac{2}{3}\, S_{MS} \qquad\qquad S_{D1} = \tfrac{2}{3}\, S_{M1}$$

These design values are used to construct the design response spectrum.

### Shortcut Tables 5.3 and 5.4 and the reverse calculation

In practice, the spectral accelerations come from the **USGS tool** (earthquake.usgs.gov design maps) or the ASCE 7 design tool. For the exam, **Tables 5.3 and 5.4** go directly from the mapped values + Site Class to the design values, with interpolation and all superscripts already programmed in:[[cite n="10" video="Chapter 5- P01 General Procedure - Design Response Spectrum - 1" time="01:52:40" page="5-9"]]
- **Table 5.3** → $S_{DS}$ (from $S_S$ and Site Class).
- **Table 5.4** → $S_{D1}$ (from $S_1$ and Site Class).

**Reverse calculation** (one-asterisk note): to recover the adjusted values from the design values, multiply by **1.5** (the inverse of 2/3): $S_{MS} = 1.5\,S_{DS}$ and $S_{M1} = 1.5\,S_{D1}$. Then the site coefficients follow: $F_a = S_{MS}/S_S$ and $F_v = S_{M1}/S_1$.

**Summary of the parameter chain:**
- **Methodical:** mapped ($S_S$, $S_1$ from Figs 22-1/22-2) → site coefficients $F_a$, $F_v$ (Table 5.2, knowing Site Class) → adjusted ($S_{MS} = F_a S_S$, $S_{M1} = F_v S_1$) → design ($S_{DS} = \tfrac{2}{3}S_{MS}$, $S_{D1} = \tfrac{2}{3}S_{M1}$).
- **Shortcut:** mapped ($S_S$, $S_1$) → design directly (Tables 5.3, 5.4) → backward for adjusted ($S_{MS} = 1.5\,S_{DS}$, $S_{M1} = 1.5\,S_{D1}$) → site coefficients ($F_a = S_{MS}/S_S$, $F_v = S_{M1}/S_1$).

The shortcut tables are faster for the exam (no interpolation, superscripts pre-baked) — just read carefully per the double/triple/four-asterisk columns. These are the first five of the six steps; **Step 6** (constructing the spectrum) follows.

### Step 6 — the design response spectrum: zones and the three transition periods

The **design response spectrum** is the relationship between the spectral acceleration $S_a$ (the maximum acceleration the building experiences) and the building's fundamental period $T$ (*the spectrum & smoothing from Ch 3*).[[cite n="11" video="Chapter 5- P02 General Procedure - Design Response Spectrum - 2" time="00:00:02" page="5-7"]] It has **four segments** distinguished by **three distinct periods** ($T_0$, $T_S$, $T_L$), and is divided into **three zones** (referencing Figure 3.7 from Chapter 3):

- **Constant acceleration zone** (pink): the maximum spectral acceleration $S_a$ is essentially constant.
- **Constant velocity zone** (green): the maximum spectral velocity $S_v$ is essentially constant.
- **Constant displacement zone** (light blue): the maximum spectral displacement $S_d$ is essentially constant.

The three distinct periods:
- **$T_0$** — constant-acceleration transition period (ascending straight line → constant acceleration).
- **$T_S$** — constant-velocity transition period (constant acceleration → constant velocity).
- **$T_L$** — constant-displacement transition period; the code renames this the **"long-period transition period"** (transitioning toward high-rise / multi-story structures).

### The four segments of the spectrum (equations) and the design PGA

The four segments and their equations:[[cite n="12" video="Chapter 5- P02 General Procedure - Design Response Spectrum - 2" time="00:08:49" page="5-8"]]

- **Segment 1 — ascending straight line**, for $T \le T_0$: $\;S_a = S_{DS}\left(0.4 + 0.6\,\dfrac{T}{T_0}\right)$, where $T_0 = 0.2\,\dfrac{S_{D1}}{S_{DS}}$.
- **Segment 2 — constant acceleration**, for $T_0 < T \le T_S$: $\;S_a = S_{DS}$, where $T_S = \dfrac{S_{D1}}{S_{DS}}$.
- **Segment 3 — curve 1**, for $T_S < T \le T_L$: $\;S_a = \dfrac{S_{D1}}{T}$.
- **Segment 4 — curve 2**, for $T > T_L$: $\;S_a = \dfrac{S_{D1}\,T_L}{T^2}$.

$T_L$ is read from ASCE 7 Figures 22-14 to 22-17 (the handout has Figure 22-14 for California): the contour-zone number at the building's latitude/longitude is $T_L$ in seconds. In California, $T_L$ ranges from **6 to 16 s** (e.g., 12 s at one location, 6 s at another).

**Design peak ground acceleration:** at $T = 0$ (the period of the ground itself — no structure), the straight-line equation reduces to $S_a = 0.4 \times S_{DS}$. This is the **design PGA** (the first point on the spectrum), equal to $S_{DS}/2.5$ = 40% of $S_{DS}$ (*consistent with Ch 4*).

### The site-specific procedure — site response versus ground motion hazard analysis

The **site-specific procedure** is **ASCE 7 Chapter 21**. It may be used for **any** structure without limitation, and becomes **mandatory** when the general procedure cannot be used. Two types of analysis:[[cite n="13" video="Chapter 5- P02 General Procedure - Design Response Spectrum - 2" time="00:33:30" page="5-11"]]

- **Site response analysis:** the geologist provides the ground motion at the **rock site** (deep down); software propagates that acceleration up through the soil layers to the **free field** (original ground) to give the design ground motion.
- **Ground motion hazard analysis:** what the code writers did — develop fragility curves and hazard maps, perform the **risk integral**, and arrive at the spectral accelerations. Either **probabilistic** (ground motions from all around the world) or **deterministic** (only nearby faults — e.g., San Andreas, Hayward, Rodgers in the Bay Area).

Knowing how to **perform** these analyses is above exam level; you only need to know **when** each is required.

### When site response analysis is required (Site Class F and its exceptions)

**Site response analysis is required by default for any structure on Site Class F** (problematic soils). **EXCEPTIONS** — the general procedure may still be used if **any one** of three conditions is satisfied:[[cite n="14" video="Chapter 5- P02 General Procedure - Design Response Spectrum - 2" time="00:39:14" page="5-11"]]

1. A structure with fundamental period $\le 0.5$ s on **liquefiable soil**: take Site Class from Table 5.1 and $F_a$, $F_v$ from Table 5.2.
2. **Highly plastic clay** (PI > 75) with layer thickness > 25 ft: **remove that layer**; if the remainder classifies as Site Class D or E, then (2-1) get $F_a$, $F_v$ from Table 5.2 for D or E and **multiply by an amplification factor** that varies linearly from **1.0 at PI = 75 to 1.3 at PI = 125**; and (2-2) the resulting $S_{DS} \le 0.33$ and $S_{D1} \le 0.133$.
3. **Very thick soft-to-medium stiff clay** (thickness > 120 ft, $s_u$ < 1,000 psf): (3-1) get $F_a$, $F_v$ from Table 5.2 for Site Class E; and (3-2) $S_{DS} \le 0.33$ and $S_{D1} \le 0.133$.

### When ground motion hazard analysis is required; the leeway and superscripts

**Ground motion hazard analysis is required in three situations:**[[cite n="15" video="Chapter 5- P02 General Procedure - Design Response Spectrum - 2" time="00:50:00" page="5-12"]]

1. **Seismically isolated structures and structures with damping systems** at sites with $S_1 \ge 0.6\,g$. (Isolated structures use lead-rubber or friction-pendulum isolators that dissipate the energy so the building stays intact; damping systems use passive devices that absorb the energy without damaging beams/columns.)
2. Structures on **Site Class E** with $S_S \ge 1$.
3. Structures on **Site Class D and E** with $S_1 \ge 0.2$.

**LEEWAY:** ground motion hazard analysis is **NOT required** (the general procedure may be used) — **EXCEPT** for the first condition (isolated / damping systems with $S_1 \ge 0.6\,g$), which is **mandatory with no exception**. The relaxations for conditions 2 and 3 are exactly the **Table 5.2 superscripts**:
- **Superscript c** (Site Class E, $S_S \ge 1$): use $F_a = 1.2$ instead of a site-specific analysis.
- **Superscript d** (Site Class E, $S_1 \ge 0.2$): not required when $T \le T_S$ and the ELF procedure is used.
- **Superscript b** (Site Class D, $S_1 \ge 0.2$): use the conservative table numbers together with the **modified design response spectrum** (extend the plateau to $1.5\,T_S$ and increase both descending branches by 50%).

### Fundamental period — why it is needed; Method 1 ($T_a = C_t\,h_n^x$)

The **fundamental period** $T$ is needed to read the spectral acceleration $S_a$ off the design response spectrum; then the base shear $V = S_a \times W$.[[cite n="16" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:00:17" page="5-13"]] The period is influenced by the **stiffness and height** of the structure — fundamentally $T = 2\pi\sqrt{\dfrac{W}{g\,k}}$ (*the SDOF period from Ch 3*). ASCE 7 §12.8.2 provides **four methods**.

**Method 1 — general approximate method** (ASCE 7 Eq 12.8-7):

$$T_a = C_t \times h_n^{\,x}$$

- $h_n$ = height in feet from the base to the roof, **NOT** including any parapet or penthouse.
- $C_t$ and $x$ are empirical coefficients (ASCE 7 Table 12.8-2), depending on the SFRS:

| SFRS | $C_t$ | $x$ |
|---|---|---|
| Steel moment-resisting frame | 0.028 | 0.8 |
| Concrete moment-resisting frame | 0.016 | 0.9 |
| Steel EBF, or steel EBF + SMF dual system, or steel BRBF | 0.03 | 0.75 |
| All other structures | 0.02 | 0.75 |

### Method 2 — $T_a = 0.1N$ for moment-resisting frames

**Method 2 — approximate method specifically for moment-resisting frames** (legacy equation, *the $T \approx 0.1N$ rule from Ch 2*):[[cite n="17" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:08:24" page="5-13"]]

$$T_a = 0.1 \times N, \quad \text{where } N = \text{number of stories}$$

Only permitted when the SFRS is a moment-resisting frame **and** both: (1) number of stories above the base $\le 12$; (2) average story height $\ge 10$ ft.

**Worked example** (Figure 5.3a): a 4-story structure with story heights 16, 9, 9, 9 ft. $N = 4 \le 12$ ✓. Average story height = $(16+9+9+9)/4 = 10.75$ ft $\ge 10$ ✓. Both satisfied → $T_a = 0.1 \times 4 = 0.4$ s.

**Exam rule:** if the question gives the material (steel or concrete moment frame), use **Method 1** ($C_t = 0.028$ or $0.016$). If the material is **not** given (just "moment-resisting frame"), use $T_a = 0.1N$ (it applies to either material), provided the two conditions are met.

### Method 3 — approximate period for shear-wall structures ($C_w$)

**Method 3 — approximate method for masonry or concrete shear-wall structures** (Eqs 12.8-9 and 12.8-10):[[cite n="18" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:13:39" page="5-14"]]

$$T_a = \frac{0.0019}{\sqrt{C_w}}\, h_n \qquad\qquad C_w = \frac{100}{A_B} \sum_{i=1}^{x} \frac{A_i}{1 + 0.83\left(\dfrac{h_n}{D_i}\right)^2}$$

- $h_n$ = base-to-roof height (no parapet/penthouse).
- $A_B$ = area of the base of the structure (plan length $L$ × width $B$).
- $x$ = number of shear walls in the direction considered.
- $A_i$ = web area of shear wall $i$ = length $D_i$ × thickness $t_i$ (for flanged T-, L-, or U-shaped walls, use the **web** area, not the flange).
- $D_i$ = length of shear wall $i$.

**Exam rule:** only use Eqs 12.8-9/12.8-10 when the question **explicitly** directs it (a long, cumbersome calculation). If the question is silent, use the Method 1 "all other structures" case ($C_t = 0.02$, $x = 0.75$) for the concrete/masonry shear wall instead.

### Method 4 — rational analysis (the Rayleigh method)

**Method 4 — rational analysis** (the code's "properly substantiated analysis"). Instead of the semi-empirical approximate methods, the period may be **computed**. One option is the **Rayleigh method**:[[cite n="19" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:23:05" page="5-15"]]

$$T_{rational} = 2\pi \sqrt{\frac{\sum w_i\,\delta_i^2}{g \sum F_i\,\delta_i}}$$

- $w_i$ = weight at level $i$; $\delta_i$ = displacement at level $i$ produced by lateral forces $F_i$; $g$ = gravitational acceleration (32.2 ft/s² = 386 in/s²).
- This is the SDOF equation $T = 2\pi\sqrt{W/(g\,k)}$ extended to multi-story, since force/deflection = stiffness $k$.

Another option is a **modal/dynamic analysis** (software solving the eigenvalue/eigenvector problem).

### Upper bound on the rational period ($C_u\,T_a$); use the larger of $T_a$ or $T_{rational}$

A rationally computed period $T_{rational}$ **cannot exceed** $C_u \times T_a$, where $T_a$ is the Method 1 approximate period and $C_u$ is a function of $S_{D1}$ (Table 5.5):[[cite n="20" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:30:47" page="5-16"]]

| $S_{D1}$ | $C_u$ |
|---|---|
| $\ge 0.3$ | 1.4 |
| $0.2$ | 1.5 |
| $0.15$ | 1.6 |
| $\le 0.1$ | 1.7 |

**Why the cap:** a longer period gives a smaller spectral acceleration → a smaller, more economical base shear (smaller members). The code caps $T_{rational}$ so engineers cannot drive the period up unrealistically (e.g., assuming partially flexible connections plus soil-structure interaction) and thereby under-design.

**Design rule:** use the **LARGER** of $T_a$ or $T_{rational}$, provided it does not exceed the upper bound $C_u\,T_a$.
- Example: $T_a = 0.7$, $T_{rational} = 0.9$, cap $C_u T_a = 1.1$ → use **0.9** (the larger, below the cap).
- Example: $T_a = 0.7$, $T_{rational} = 1.2$, cap $C_u T_a = 1.1$ → use **1.1** (1.2 exceeds the cap).

### Seismic Design Category — what it controls and what is needed

The **Seismic Design Category (SDC)** reflects the seismic risk and controls the permitted SFRS, height limitations, the permitted lateral analysis procedure, restrictions on irregular buildings, and non-structural component detailing (*Ch 4, Table 4.2: A very low, B low, C moderate, D moderate-to-high, E/F high*).[[cite n="21" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:44:01" page="5-17"]]

To determine the SDC you need: the **Risk Category** (I–IV, IBC Table 1604.5, best read from book pages 4-9/4-10), the mapped long-period acceleration $S_1$, and the design accelerations $S_{DS}$ and $S_{D1}$.

### Determining the SDC from Table 5.6

Reading **Table 5.6** (replica of IBC 1613.3.5.1/.2 and ASCE 7 Tables 11.6-1/11.6-2):[[cite n="22" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:47:25" page="5-17"]]
- **Step 1 — start from the LAST row**, checking $S_1$: if $S_1 \ge 0.75$ and Risk Category I/II/III → **SDC E**; if $S_1 \ge 0.75$ and Risk Category IV → **SDC F**.
- **Steps 2–3 — if $S_1 < 0.75$:** determine the SDC **twice** (once from the $S_{DS}$ column, once from the $S_{D1}$ column) and choose the **MORE STRINGENT** (higher letter).

**Worked example:** $S_1 = 0.4$ (< 0.75), so determine twice. $S_{DS} = 0.55$, Risk Category III: $0.55 \ge 0.5$ → SDC D. $S_{D1} = 0.14$, Risk Category III: $0.14$ is between $0.133$ and $0.2$ → SDC C. Choose the higher → **SDC D**.

### SDC leeway — SDC A criteria and the $S_{DS}$-only determination

**Leeway notes:**[[cite n="23" video="Chapter 5- P03 Fundamental Period, Seismic Design Category" time="00:54:39" page="5-17"]]
- A structure is assigned **SDC A** (very low seismic risk) when both $S_1 \le 0.04$ and $S_S < 0.15$ (in addition to the table conditions $S_{DS} < 0.067$ and $S_{D1} < 0.067$).
- When $S_1 < 0.75$, the SDC is permitted to be determined based **only on $S_{DS}$** (skipping the $S_{D1}$ check), provided **all four** conditions are met: (1) the approximate period $T_a$ in both directions is less than $0.8\,T_S$; (2) the rational period $T_{rational}$ in both directions is less than $T_S$; (3) the seismic response coefficient $C_s$ is taken as the constant-acceleration value $S_{DS}\,I_e / R$; (4) the diaphragms are rigid (concrete slabs), or for flexible diaphragms the distance between vertical elements does not exceed 40 ft. (Here $T_S = S_{D1}/S_{DS}$, the constant-velocity transition period, normally < 1.)

### The six major SFRS categories (Table 12.2-1)

**ASCE 7 §12.2, Table 12.2-1** classifies building types by how they resist lateral/seismic forces. There are **six major categories**:[[cite n="24" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:00:35" page="5-18"]]
- **Category A** — Bearing wall system.
- **Category B** — Building frame system.
- **Category C** — Moment-resisting frames.
- **Category D** — Dual system with a special moment frame.
- **Category E** — Dual system with an intermediate moment frame.
- **Category G** — Cantilevered column system.

Two additional, less-common categories are listed but are **not used for seismic resistance**: the **shear wall-frame interactive system** (low seismicity only — not permitted for SDC C, D, E, or F) and **steel systems not specifically detailed for seismic resistance** (not permitted for SDC D, E, or F).

Each category is further classified by **material** and by the **level of connection detailing** — ordinary (OMF), intermediate (IMF), or special (SMF). Both the **system limitation** (whether a system may be used at all) and the **height limitation** depend on the SDC.

### Category A — bearing wall system

The **same wall element** resists both the gravity (vertical) load and the lateral seismic load.[[cite n="25" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:05:00" page="5-21"]] In seismic design we accept damage at the wall-to-foundation connection, but if that damage is extensive it may compromise the wall's ability to carry gravity load — a **lack of redundancy** (one element doing both jobs). Materials: reinforced concrete, plain concrete (no reinforcement), masonry, or light frame; special or ordinary detailing. **Popular, but low redundancy.**

### Category B — building frame system

**Separate** systems for gravity and lateral.[[cite n="26" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:08:47" page="5-22"]] Gravity is carried by a **"space frame"** — beams and columns with **simple** (non-moment, non-rigid) connections that carry no moment (e.g., a steel beam bolted to a column flange with an angle). The lateral seismic load is carried by an **independent shear wall or braced frame** → **better redundancy**. The shear wall may be reinforced concrete, masonry, steel-plate, or wood light frame; the braced frame may be concentrically braced (CBF) or eccentrically braced (EBF), and the brace material is always steel.

### Category C — moment-resisting frame

Beam-to-column connections are **rigid (moment) connections** (in steel: complete-penetration welds at the flanges plus continuity plates framing the joint).[[cite n="27" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:12:42" page="5-22"]] The same frame carries both gravity and lateral load — but unlike the bearing wall it is **highly redundant**: the lateral load is resisted by flexural (inelastic) deformation at many rigid connections, so if one connection yields, the load redistributes to the others.
- **Advantage:** very redundant (many rigid connections sharing the load).
- **Disadvantage:** very flexible (low stiffness) — it deflects a lot, which can destroy sensitive equipment (e.g., hospital medical equipment).

Material: steel or reinforced concrete; detailing: ordinary (OMF), intermediate (IMF), or special (SMF).

### Category D — dual system with a special moment frame

Combines a **building frame system** (shear wall, CBF, or EBF) with a **special moment frame (SMF)** — getting the **stiffness** of the building frame plus the **redundancy** of the moment frame.[[cite n="28" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:20:24" page="5-23"]] The total seismic force is distributed between the building frame (primary) and the moment frame (secondary) **in proportion to their relative rigidity**. This is the **best system available — NO height limitation.** To qualify as a dual system: (1) it must combine a building frame system with a moment-resisting frame; and (2) the moment frame must be designed to be **capable of resisting at least 25% of the seismic forces**.

### Category E — dual system with an intermediate moment frame

Same as Category D, but the moment frame is an **intermediate moment frame (IMF)** — intermediate (less stringent) seismic detailing of the rigid connections.[[cite n="29" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:28:36" page="5-23"]] Building frame (shear wall, CBF, or EBF) is primary, the IMF is secondary, force distributed in proportion to rigidity. This is the **second-best system** — it has **some height limitations by SDC**. The IMF must also be designed to be capable of resisting **at least 25%** of the seismic forces.

### Category G — cantilevered column system

A **cantilevered column system (inverted pendulum)**: lumped masses supported on flexible cantilever columns, modeled as a single-degree-of-freedom system (*the SDOF of Ch 3*).[[cite n="30" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:31:59" page="5-24"]] The **same** cantilever columns carry both gravity and lateral load. It has the **least stiffness** of all systems and limited redundancy, so the total structural height is **limited to 35 ft**. Popular for house garages and gas-station canopies/sheds.

### Reading Table 12.2-1 — system/height limitations (NP/NL), footnotes, and methodology

In the "structural system limitations including structural height" column, indexed by SDC (B, C, D, E, F):[[cite n="31" video="Chapter 5- P04 SFRS - System and Height Limitations" time="00:36:59" page="5-25"]]
- **NP** = Not Permitted — the system may **not** be used for that SDC.
- **NL** = Not Limited — the system may be used with **no height limit**.
- **A number** = the system may be used, with that **maximum structural height in feet**.

**Footnotes** (last page of the table) can **increase** the tabulated heights under specific conditions (a superscript on the height value refers to a footnote):
- **Steel ordinary concentric braced frames:** permitted in single-story buildings up to a structural height of **60 ft** (instead of the tabulated 35 ft) where the roof dead load $\le 20$ psf, and in penthouse structures.
- **Intermediate precast shear walls:** increase the structural height $h_n$ to **45 ft** (from 40 ft) for single-story warehouse facilities.
- **Other footnotes** (steel EBF, steel special CBF, BRBF, steel-plate shear wall, special reinforced concrete wall): complicated nested requirements to raise a tabulated height — not worth focusing on for the exam.

**Methodology for reading the table (be methodical):**
1. Determine the **SDC** of the building.
2. Identify the **SFRS** (bearing wall / building frame / moment frame / dual w/ SMF / dual w/ IMF / cantilevered column).
3. Identify the **sub-type** (shear wall / braced frame — CBF or EBF).
4. Identify the **material** (concrete, wood, steel, masonry).
5. Identify the **detailing level** (ordinary, intermediate, or special).

### Hysteretic behavior — accepting yielding, the hysteresis cycle, and ductility

It is uneconomical to keep a building entirely elastic after a major earthquake (*the design philosophy from Ch 4*).[[cite n="32" video="Chapter 5- P05 SFRS Characteristics- R, Omega, Cd" time="00:01:24" page="5-25"]] Instead, **limited structural damage (yielding)** is allowed at predetermined locations designed, detailed, and constructed to dissipate the earthquake energy **without collapse** and without impairing the gravity load-carrying capacity.

Under cyclic seismic loading the structure undergoes successive loading/unloading, and the force-displacement relationship follows a sequence of **hysteresis loops**. The **area enclosed** by these loops is the nonlinear hysteretic energy absorption (the energy dissipated during the earthquake).

Consider a reinforced-concrete cantilever shear wall under lateral seismic force (force-displacement curve from origin O):
- From O up to point A the response is **elastic** — remove the force and the wall returns upright, no permanent deformation.
- At point A the reinforcement **yields** — the wall reaches its maximum capacity $V_m$ and cannot develop more force; it keeps deflecting along a horizontal plateau (inelastic/plastic behavior, accepted damage, with concrete cracking and spalling on the tension side).
- When the ground motion reverses, the wall **unloads** and loads the opposite direction; if the force returns to zero with the wall still tilted, that is **permanent deformation** (sometimes corrected after the event by pushing the building upright with a crane).
- The cycle repeats until shaking stops.

All materials — concrete, steel, wood, masonry — exhibit these loops. **Larger enclosed area = more energy dissipated = more ductility:** "fat"/wide loops = ductile; "skinny"/pinched loops = less ductile (Figure 5.5; idealized as straight lines but actually nonlinear curves).

### Response modification coefficient $R$ — reducing the elastic force

From the design response spectrum, the spectral acceleration × weight gives a very large **elastic** seismic force $V_E$ (e.g., 1,000 kips, *the $V = m\,S_a$ base shear from Ch 3*).[[cite n="33" video="Chapter 5- P05 SFRS Characteristics- R, Omega, Cd" time="00:23:40" page="5-26"]] Designing for $V_E$ keeps the structure essentially elastic but is uneconomical. Because the structure can accept damage without collapsing, the force is **reduced by dividing by $R$**:

$$V = \frac{V_E}{R} \quad \left(\text{e.g., } \frac{1000}{8} = 125 \text{ kips}\right)$$

The building is designed for the much smaller prescribed force $V$; under the real earthquake it yields and dissipates energy through hysteresis. $R$ does two things: (1) it **reduces** the design seismic force from the elastic level $V_E$ to the prescribed design force $V$; and (2) it **modifies** the structural response from elastic to inelastic.

### What $R$ depends on — ductility, redundancy, and past performance

The value of $R$ depends on three factors:[[cite n="34" video="Chapter 5- P05 SFRS Characteristics- R, Omega, Cd" time="00:31:10" page="5-27"]]
1. **System ductility** — the ability to absorb energy and sustain cyclic inelastic deformations without collapse.
2. **Redundancy** — the ability to redistribute load to other resisting elements upon yielding, or a backup/secondary system (the many rigid connections of a moment frame, or the primary/secondary systems of a dual system).
3. **Observed performance** of the material and system in past earthquakes (verified by instrumenting new buildings).

In general, a larger $R$ indicates higher ductility, higher redundancy, and robust past performance. **Definitions:** **ductility** = the capability of a system to deform and yield without collapse (the opposite of brittle); **redundancy** = the ability of structural elements, after yielding, to redistribute loads to different resisting elements.

$$R = \frac{V_E}{V} = \frac{\text{theoretical elastic base shear}}{\text{prescribed design base shear}}$$

Brittle, lightly detailed systems get a **low** $R$; ductile materials with special detailing get a **high** $R$ (more enclosed hysteresis area). Values from Table 12.2-1, e.g., steel special moment frame $R = 8$; steel ordinary moment frame $R = 3.5$. **Exam note:** a question may relate the enclosed hysteresis area to $R$ — more area = more energy dissipated = more ductility = larger $R$.

### Overstrength factor $\Omega_0$ and its sources

The structure is designed to **begin yielding** at the prescribed design force $V$. In reality it sustains a much larger force $V_m$ before yielding:[[cite n="35" video="Chapter 5- P05 SFRS Characteristics- R, Omega, Cd" time="00:44:16" page="5-28"]]

$$V_m = \Omega_0 \times V \quad (\text{e.g., } 3 \times 125 = 375 \text{ kips})$$

$V_m$ is the maximum (actual) inelastic-response seismic force. $\Omega_0$ accounts for the **overstrength / reserve capacity** inherent in the design process. Sources:
- Member sizes in excess of the minimum required (a column designed at 19″×19″ but built at 24″×24″).
- Higher energy dissipation capacity than estimated.
- Conservative material resistance ($\phi$) factors ($\phi = 0.9$ for steel reinforcement, $0.85$ for concrete).
- Actual material strengths exceeding nominal (rebar nominal $f_y = 60$ ksi but actually ~68–76 ksi; concrete nominal $f'_c = 4{,}000$ psi but actually 5,000–6,000 psi).

Values from Table 12.2-1 (steel special moment frame: $R = 8$, $\Omega_0 = 3$, $C_d = 5.5$). **Footnote:** where the tabulated $\Omega_0 \ge 2.5$, it may be **reduced by 0.5** for structures with flexible diaphragms (wood diaphragms).

### Deflection amplification factor $C_d$

Using the prescribed design force $V$, the deflection is $\delta_{xe} = V/k$ (force over stiffness) — the **theoretical elastic** deflection (e.g., 2 in).[[cite n="36" video="Chapter 5- P05 SFRS Characteristics- R, Omega, Cd" time="00:58:10" page="5-29"]] But the building yields beyond $V$ and actually deflects more. The **actual (amplified, inelastic-response) deflection** is:

$$\delta_x = C_d \times \delta_{xe} \quad (\text{e.g., } 5.5 \times 2 = 11 \text{ in})$$

- $\delta_{xe}$ = theoretical elastic deflection (subscript $e$ = elastic); $\delta_x$ = actual deflection (no $e$); subscript $x$ = the level along the height.
- $C_d = \delta_x / \delta_{xe}$ (from Table 12.2-1; steel special moment frame $C_d = 5.5$).
- Including the importance factor, the code form is $\delta_x = \dfrac{\delta_{xe}\,C_d}{I_e}$.

$\delta_x$ has three names: the **actual**, the **amplified**, or the **inelastic-response** displacement; it is the design displacement.

### Combining SFRS — overview and combination in different directions

A building often uses more than one SFRS. This part covers which $R$, $\Omega_0$, and $C_d$ to use when systems are combined.[[cite n="37" video="Chapter 5- P06 SFRS Combinations" time="00:00:21" page="5-30"]] **In all cases $\Omega_0$ and $C_d$ FOLLOW whichever $R$ is chosen** for the design.

**Combination in different directions:** design each direction independently, each with its own $R$ (and corresponding $\Omega_0$, $C_d$). Example: special reinforced concrete shear walls N-S ($R = 6$) and steel special moment frames E-W ($R = 8$). Design N-S with $R = 6$ and E-W with $R = 8$, independently.

### Same-direction vertical combination — Conditions 1 and 2

When different systems resist forces in the **same direction**, the **more stringent** system limitation and height limitation applies. Two cases: vertical and horizontal.[[cite n="38" video="Chapter 5- P06 SFRS Combinations" time="00:06:45" page="5-31"]]

**Vertical combination — same direction, along the height** (Figure 5.8):
- **Condition 1** (Fig 5.8a): the **lower** system has the **lower** $R$. Example: special reinforced masonry shear wall ($R = 5.5$) in stories 1–3, concrete moment frame ($R = 8$) in stories 4–6. **Rule:** design the upper for the upper ($R = 8$ with its $\Omega_0$, $C_d$) and the lower for the lower ($R = 5.5$, $\Omega_0 = 2.5$, $C_d = 4$). Forces transferred from the upper to the lower SFRS are **increased** by multiplying by $\dfrac{R_{\text{higher}}}{R_{\text{lower}}} = \dfrac{8}{5.5}$.
- **Condition 2** (Fig 5.8b): the **upper** system has the **lower** $R$. Example: concrete moment frame ($R = 8$) in stories 1–3, special reinforced masonry shear wall ($R = 5.5$) in stories 4–6. **Rule:** **both** upper and lower are designed using the **smaller** $R$ ($5.5$, with $\Omega_0 = 2.5$, $C_d = 4$).

### Vertical combination — combined conditions and exceptions

**Combination of Conditions 1 and 2** (Fig 5.8c): work **from the top down**, comparing two systems at a time. The $R$ used in design **cannot increase** as you go down the height.[[cite n="39" video="Chapter 5- P06 SFRS Combinations" time="00:16:30" page="5-31"]] Example (6-story): concrete MF $R = 8$ in stories 1–2, special reinforced masonry SW $R = 5.5$ in stories 3–4, concrete MF $R = 8$ in stories 5–6. Top pair (5–6 vs 3–4) is Condition 1 → design 5–6 with $R = 8$, 3–4 with $R = 5.5$. Next pair (3–4 vs 1–2) is Condition 2 → controlled by the smaller $R = 5.5$, so stories 1–2 use $R = 5.5$ (it cannot rise back to 8).

**Exceptions (no vertical combination required):** (1) rooftop structures ≤ 2 stories and ≤ 10% of the total structure weight; (2) other supported structural systems weighing ≤ 10% of the total structure weight; (3) detached one- and two-story dwellings of light-frame construction.

### Two-stage analysis — flexible upper portion over rigid lower portion

**Two-stage analysis** (ASCE 7 §12.2.3.2; Fig 5.8d) is permitted for a structure with a **flexible upper portion over a rigid lower portion** (e.g., a high-rise tower over a shopping mall or parking garage).[[cite n="40" video="Chapter 5- P06 SFRS Combinations" time="00:23:38" page="5-32"]] The upper and lower portions may be analyzed independently as separate structures, then the force is transferred from upper to lower. **All five conditions** must be met:
1. The stiffness of the lower portion is **at least 10 times** the stiffness of the upper portion.
2. The period of the entire structure does not exceed **1.1 times** the period of the upper portion considered as a separate structure fixed at the base.
3. The upper portion is designed as a separate structure using its appropriate $R$ and redundancy factor $\rho$.
4. The lower portion is designed as a separate structure using its appropriate $R$ and redundancy factor $\rho$.
5. The reactions from the upper portion are multiplied by the ratio $\dfrac{(R/\rho)_{\text{upper}}}{(R/\rho)_{\text{lower}}}$, and this ratio shall **not** be taken less than 1.

### Horizontal combination — different lines of resistance

**Horizontal combination — same direction, along different lines of resistance** (Fig 5.9a).[[cite n="41" video="Chapter 5- P06 SFRS Combinations" time="00:35:17" page="5-34"]] Example (N-S): lines 1 and 4 are special reinforced concrete shear walls ($R = 6$); lines 2 and 3 are steel ordinary moment frames ($R = 3.5$). **General rule:** $R$ shall not be greater than the **lowest** value of $R$ of any system in that direction → use $R = 3.5$; $\Omega_0$ and $C_d$ consistent with the governing $R$.

**Exception** (Fig 5.9b): each line may be designed for **its own** $R$ if **all** of the following are met: (1) Risk Category I or II; (2) two stories or less above the grade plane; (3) light-frame construction or flexible diaphragms. Example: lines 1 and 4 steel special plate shear wall ($R = 7$), lines 2 and 3 steel special concentrically braced frame ($R = 6$) → design each line with its own $R$. **However, the diaphragm itself shall be designed using the least value of $R$** (= 6).

### Regular versus irregular structures

A structure's plan shape and configuration greatly affect its seismic performance (ASCE 7 §12.3.2).[[cite n="42" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:01:17" page="5-36"]] A **regular** structure has uniform stiffness and mass distribution along the height plus symmetrical geometry (like a box). An **irregular** structure has significant physical discontinuity (in plan or elevation) and non-uniform mass and stiffness. The choice of analysis procedure (the **ELF static method** vs a **dynamic procedure** — modal response spectrum or time history) depends on whether the structure is regular or irregular and on the severity. There are **five horizontal** and **five vertical** irregularities.

### Horizontal irregularities — torsional (1a/1b) and reentrant corner (2)

**Five Horizontal Irregularities** (Table 5.8):[[cite n="43" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:05:09" page="5-36"]]

**Type 1a / 1b — Torsional / Extreme torsional:** applying the seismic force to the diaphragm causes rotation, producing a story drift on each side (the maximum $\delta_{max}$ and minimum $\delta_{min}$). The average story drift $\delta_{avg} = \dfrac{\delta_{max} + \delta_{min}}{2}$. (Story drift = the difference between the deflection at the top and bottom of a story.)
- **Type 1a** (torsional): $\delta_{max} > 1.2 \times \delta_{avg}$ (including accidental torsion).
- **Type 1b** (extreme torsional): $\delta_{max} > 1.4 \times \delta_{avg}$.

**Type 2 — Reentrant corner:** a corner cut where **both** plan projections beyond the corner exceed **15%** of the corresponding plan dimension of the main diaphragm. *(Penalty for SDC D, E, F.)*

### Horizontal irregularities — diaphragm discontinuity, out-of-plane offset, nonparallel

**Type 3 — Diaphragm discontinuity:** a diaphragm with an open area greater than **50%** of the gross enclosed diaphragm area, **or** a change in diaphragm stiffness (e.g., thickness — stiffness $\propto E\,A$) of more than **50%** from one story to the next (e.g., a 12-in diaphragm over a 4-in diaphragm). *(Penalty for SDC D, E, F.)*[[cite n="44" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:11:52" page="5-37"]]

**Type 4 — Out-of-plane offset:** a discontinuity in the lateral-force path, such as an **out-of-plane offset** of at least one vertical SFRS element (shear walls, moment frames, braced frames not aligned in the vertical plane). *(Penalty for SDC B through F.)*

**Type 5 — Nonparallel system:** the vertical SFRS elements are **not parallel** to the major (orthogonal) axes of the building. *(Penalty for SDC B through F.)*

### Vertical irregularities — soft story (1a/1b) and weight (2)

**Five Vertical Irregularities** (Table 5.9):[[cite n="45" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:20:33" page="5-38"]]

**Type 1a / 1b — Soft story / Extreme soft story (based on STIFFNESS):** compare a story's lateral stiffness to the story **above** only (story stiffness = sum of the column/brace/wall stiffnesses; stiffness = force/deflection, *Ch 3*).
- **Type 1a** (soft story): a story's stiffness < **70%** of the story above, **or** < **80%** of the average of the three stories above.
- **Type 1b** (extreme soft story): < **60%** of the story above, **or** < **70%** of the average of the three stories above.

*(Penalty for SDC D, E, F.)*

**Type 2 — Weight (mass) irregularity:** the effective mass of any level is more than **150%** of the mass of an **adjacent** level (above or below). A roof lighter than the floor below is not considered. *(Penalty for SDC D, E, F.)*

### Vertical irregularities — geometric, in-plane discontinuity, weak story (5a/5b)

**Type 3 — Vertical geometric discontinuity:** the horizontal dimension of the **SFRS** (not the building) changes by more than **130%** from one story to an adjacent story. *(Penalty for SDC D, E, F.)*[[cite n="46" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:29:24" page="5-39"]]

**Type 4 — In-plane discontinuity in vertical SFRS elements:** an offset of the vertical SFRS **within the same vertical plane** that results in overturning demands on supporting elements (a beam, column, truss, or slab). Example: a second-story shear wall offset from the first-story shear wall (within the plane) forces an underlying column to carry the overturning tension force, making it part of the SFRS. *(Penalty for SDC B through F.)*

**Type 5a / 5b — Weak story / Extreme weak story (based on STRENGTH):** compare a story's lateral strength to the story **above** only (story strength = sum of the strengths of the columns, walls, etc.).
- **Type 5a** (weak story): a story's strength < **80%** of the story above.
- **Type 5b** (extreme weak story): < **65%** of the story above.

*(Penalty for SDC D, E, F; 5b is further restricted — see below.)*

### Irregularity exceptions

**Exceptions:**[[cite n="47" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:42:21" page="5-39"]]
1. When the story drift (excluding torsion) is **not greater than 130%** of the next story above, vertical irregularities Type 1a/1b (soft / extreme soft story) and Type 2 (weight) **do not apply**.
2. For a **single-story building** (any SDC) or a **two-story building** (SDC B, C, or D), vertical irregularities Type 1a/1b and Type 2 **do not apply**.

### Limitations / prohibitions due to irregularities

**ASCE 7 §12.3.3:**[[cite n="48" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:48:24" page="5-40"]]
- **SDC B and C:** extreme weak story (vertical Type 5b) is **not permitted**, **unless** the building is ≤ 2 stories or ≤ 30 ft in structural height.
- **SDC D:** extreme weak story (Type 5b) is **not permitted**, no exception.
- **SDC E and F:** the following four are **not permitted** (cannot exist): weak story (vertical 5a), extreme weak story (vertical 5b), extreme soft story (vertical 1b), and extreme torsional (horizontal 1b).

### Type 4 horizontal versus Type 4 vertical irregularity

Both are offsets of the vertical SFRS elements (e.g., a second-story shear wall not aligned with the first-story shear wall).[[cite n="49" video="Chapter 5- P07 Horizontal and Vertical Irregularities" time="00:53:41"]] The difference: **Type 4 horizontal** is an **out-of-plane** offset; **Type 4 vertical** is an **in-plane** offset (within the same vertical plane).

### Analysis procedures and the ELF steps

There are **three methods** to analyze a building (ASCE 7 §12.6), chosen by SDC, size, geometry, irregularities, detailing, and materials.[[cite n="50" video="Chapter 5- P08 ELF- Base Shear" time="00:00:43" page="5-41"]] The **Equivalent Lateral Force (ELF)** procedure is the most common **static** method and the focus of the exam. Structures with **extreme** vertical/horizontal irregularities are **not permitted** to use ELF — they must use a **dynamic** procedure (modal response spectrum or time history). You must know how to perform ELF **and** know when it cannot be used. There is also a **simplified design procedure** (an abbreviated ELF, covered later).

**ELF steps:** (1) seismic base shear $V$; (2) vertical distribution of $V$ into concentrated forces $F_x$; (3) story shear and overturning moment; (4) story drift, P-Delta effect, building separation; (5) orthogonal interaction; (6) ELF limitations.

### Step 1 — base shear $V = C_s W$ and the $C_s$ code equations (default, upper, lower limits)

**Step 1 — Seismic Base Shear** (*the $V = C_s W$ from Ch 3*):[[cite n="51" video="Chapter 5- P08 ELF- Base Shear" time="00:06:10" page="5-41"]]

$$V = C_s \times W$$

- $C_s$ = the **seismic response coefficient** (the fraction of the weight imparted as seismic force at the base).
- $W$ = the **effective seismic weight**.

**Seismic Response Coefficient $C_s$ — Method 1 (code equations):** start with the default, then check against an upper limit and a lower limit.
- **Default** (Eq 12.8-2): $C_s = S_{DS}\,\dfrac{I_e}{R}$, where $I_e$ = seismic importance factor (*Ch 4*) and $R$ = response modification coefficient (Table 12.2-1).
- **Upper limit (maximum):**
  - if $T \le T_L$: $\;C_s \le \dfrac{S_{D1}}{T}\cdot\dfrac{I_e}{R}$ [Eq 12.8-3]
  - if $T > T_L$: $\;C_s \le \dfrac{S_{D1}\,T_L}{T^2}\cdot\dfrac{I_e}{R}$ [Eq 12.8-4]
  
  ($T_L$ = long-period transition period, 6–16 s in California.)
- **Lower limit (minimum):**
  - $C_s \ge 0.044\,S_{DS}\,I_e$, and not less than $0.01$ [Eq 12.8-5]
  - additionally, if $S_1 \ge 0.6\,g$: $\;C_s \ge \dfrac{0.5\,S_1\,I_e}{R}$ [Eq 12.8-6]

### Seismic response coefficient $C_s$ — the shortcut via $S_a$

**Method 2 — shortcut:** read the spectral acceleration $S_a$ directly off the design response spectrum by comparing $T$ with $T_S = \dfrac{S_{D1}}{S_{DS}}$ (the constant-velocity transition period):[[cite n="52" video="Chapter 5- P08 ELF- Base Shear" time="00:11:16" page="5-42"]]
- $T \le T_S$ → $S_a = S_{DS}$ (the ascending straight line is ignored; treat as constant acceleration).
- $T_S < T \le T_L$ → $S_a = \dfrac{S_{D1}}{T}$.
- $T > T_L$ → $S_a = \dfrac{S_{D1}\,T_L}{T^2}$.

Then $C_s = S_a\,\dfrac{I_e}{R}$. With the shortcut, the **default and upper-limit checks are already built in** — only the lower-limit equations (12.8-5, 12.8-6) must still be checked. (And if $C_s$ is controlled by $S_{DS}$ — the constant-acceleration region — the lower limit need not be checked either.)

**Exam tip:** if the question gives no $S_{D1}$ and no way to compute the period, it intends the default equation $C_s = S_{DS}\,I_e/R$ (valid for 1- or 2-story buildings).

### Effective seismic weight $W$ — what to include

Start with the floor and wall **dead load**, then add the applicable portions of service load:[[cite n="53" video="Chapter 5- P08 ELF- Base Shear" time="00:26:26" page="5-42"]]
1. **25%** of the floor live load in storage areas/warehouses — **except** where the storage load adds no more than 5% of the effective seismic weight at that level, and it is **not** included for public garages / open parking structures.
2. **Office buildings:** the actual partition weight, or a minimum of **10 psf** of floor area, whichever is greater.
3. The total operating weight of any **permanent equipment** (air conditioning, fans, boilers).
4. **20%** of the uniform design snow load where the flat-roof snow load exceeds **30 psf**.
5. The weight of landscaping and materials at roof gardens and similar areas.

$W$ is determined for all items **above the base**, excluding any basement weight or any weight not contributing to the vibration of the structure (a **lumped-mass** model).

### Lumped-mass model for $W$ and the SDC A exception

**Lumped-mass examples** (Figure 5.10), using the MDOF lumped-mass idea (*Ch 3*):[[cite n="54" video="Chapter 5- P08 ELF- Base Shear" time="00:31:25" page="5-43"]]
- **One-story warehouse:** $W_1$ (at the roof/level 1) = roof dead load (weight/area × roof area) + wall dead load (the **upper half** of the wall height — tributary to the roof — × wall length × weight/area) + 20% of snow (if snow > 30 psf). The lower half of the wall goes directly to the foundation (excluded); floor live load on grade goes directly to the ground (excluded).
- **Two-story warehouse:** $W_2$ (roof/level 2) = roof DL + walls (half the story-2 height) + 20% snow. $W_1$ (floor/level 1) = floor DL + walls (half the story-2 height + half the story-1 height = the tributary height, e.g., 7 + 8 = 15 ft) + 25% of the floor live load (warehouse). The lower half of the story-1 wall and the floor live load attached to the foundation are excluded. Total $W = W_1 + W_2$.

**SDC A exception:** for SDC A (very low seismic risk), the base shear is simply **1% of $W$**, where $W$ is the dead load of the structure (no elaborate $C_s$ calculation).

### Step 2 — vertical distribution $F_x = C_{vx} V$

The base shear $V$ is distributed along the height as lateral seismic forces $F_x$ at each level (ASCE 7 §12.8.3):[[cite n="55" video="Chapter 5- P09 ELF- Fx, Vx, OTMx" time="00:00:48" page="5-44"]]

$$F_x = C_{vx} \times V, \qquad C_{vx} = \frac{w_x\,h_x^{\,k}}{\sum w_i\,h_i^{\,k}}$$

- $w_i$, $w_x$ = the portion of the total effective seismic weight at level $i$ or $x$.
- $h_i$, $h_x$ = the height from the base to level $i$ or $x$.

### The exponent $k$ — linear versus parabolic distribution and the higher modes

The exponent $k$ is related to the building period:[[cite n="56" video="Chapter 5- P09 ELF- Fx, Vx, OTMx" time="00:06:42" page="5-44"]]
- $T \le 0.5$ s → $k = 1$
- $T \ge 2.5$ s → $k = 2$
- $0.5 < T < 2.5$ s → interpolate: $k = 0.75 + 0.5\,T$

**Meaning of $k$** (Figure 5.12): $k = 1$ gives a **linear** vertical distribution of forces along the height; $k = 2$ gives a **parabolic** distribution. The parabolic distribution (larger $k$) adds lateral force at the **top** of the building to reflect the **higher modes** (*Ch 3, modal participation*). The **first (fundamental) mode** supplies **80–95%** of the total seismic response; modes 2 and higher supply about **5–20%**. The first mode has the largest period and therefore the smallest frequency (frequency = 1/period), so modes 2+ collectively have **higher frequencies** — hence "higher-frequency modes." Increasing $k$ from 1 to 2 adds force at the top to account for these. (A common theoretical exam question.) $F_x$ is applied at the **center of mass (CM)** at each level.

### Story, level, and floor nomenclature

- **Story** = the space between two levels, numbered after the **upper** level (the 4th story is between level 3 and level 4).[[cite n="57" video="Chapter 5- P09 ELF- Fx, Vx, OTMx" time="00:21:15" page="5-46"]]
- **Level** = a floor. **Seismic** nomenclature: the base = **level 0**, then level 1, 2, 3… (matching the $w$/$W$ and $F$ subscripts). **Building-industry** nomenclature: the foundation/base = the **1st floor**, then 2nd floor, etc.

**Important distinction:** the building-industry "3rd floor" = seismic "level 2." So equipment "added to the third floor" is added to $W_2$. **Exams trick on this** — convert floor designations to levels to match the equations.

### Story shear $V_x$ and overturning moment $OTM_x$

**Story shear $V_x$:** cut within the story, look up, and sum all the forces above the cut; the story shear is **constant within the story**.[[cite n="58" video="Chapter 5- P09 ELF- Fx, Vx, OTMx" time="00:26:12" page="5-46"]] Two-story example: $V_2 = F_2$; $V_1 = F_1 + F_2$.

**Overturning moment $OTM_x$:**
- **Method 1 — force × distance:** stand at the level of interest, look up, and sum (each force × the distance from where it applies to where you stand). At the top (cantilever tip), $OTM = 0$. Two-story: $OTM_2 = 0$; $OTM_1 = F_2 H_2$; $OTM_0 = F_2(H_2 + H_1) + F_1 H_1$.
- **Method 2 — story shear × story height** (building industry): $OTM$ at a level = accumulated $OTM$ from above + (story shear × story height) of the story just passed, working top down. Two-story: $OTM_1 = OTM_2 + V_2 H_2$; $OTM_0 = OTM_1 + V_1 H_1$. Both methods give the same result.

### Exam wording notes and horizontal distribution of story shear

**Exam wording notes:**[[cite n="59" video="Chapter 5- P09 ELF- Fx, Vx, OTMx" time="00:55:25" page="5-48"]]
- The "shear force **just below level 2**" is the second-story shear $V_2 = 25$ k.
- The **base shear $V$** is numerically equal to the first-story shear $V_1 = 30$ k (conceptually different but numerically equal). The base shear also equals the **sum of all $F_x$ forces** ($5 + 10 + 15 = 30$ k).

**Horizontal distribution:** the seismic design story shear (and the overturning moment increment) is applied at the **center of mass** and then distributed to the various vertical SFRS elements based on their **relative rigidity** (the detailed method is in Chapter 6).

### Definition of story drift; elastic versus inelastic deflection

**Story drift** = the difference between the lateral deflection at the **top** of a story and at the **bottom** of that story, computed at the center of mass (Figure 5.16).[[cite n="60" video="Chapter 5- P12 ELF- Story Drift" time="00:00:38" page="5-48"]] The drift of story $x$ is denoted $\Delta_x$ (capital delta): e.g., $\Delta_3$ = deflection at top of story 3 − deflection at bottom of story 3, and similarly $\Delta_2$, $\Delta_1$.

**Which deflection — elastic or inelastic?** The drift must use the **actual (amplified / inelastic-response) deflection** $\delta_x$, **NOT** the theoretical elastic deflection $\delta_{xe}$. The relationship (*the $C_d$ amplification from earlier this chapter*):

$$\delta_x = \delta_{xe}\,\frac{C_d}{I_e}$$

- $\delta_{xe}$ = theoretical elastic deflection (= force / stiffness), subscript $e$ = elastic.
- $C_d$ = deflection amplification factor (Table 12.2-1); $I_e$ = importance factor (from the Risk Category).

So $\Delta_x = (\delta_{xe,\text{top}} - \delta_{xe,\text{bottom}})\,\dfrac{C_d}{I_e}$ — pull out the common factor $C_d/I_e$, subtract the elastic deflections of the two levels, then amplify. Example: $\Delta_3 = (\delta_{e3} - \delta_{e2})\,\tfrac{C_d}{I_e}$; $\Delta_2 = (\delta_{e2} - \delta_{e1})\,\tfrac{C_d}{I_e}$; $\Delta_1 = (\delta_{e1} - 0)\,\tfrac{C_d}{I_e}$.

### Computing the elastic deflection $\delta_{xe}$; elastic drift = story shear / story stiffness

Computing the theoretical elastic deflection $\delta_{xe}$ (a structural-analysis result you must reproduce — put these on your cheat sheet):[[cite n="61" video="Chapter 5- P12 ELF- Story Drift" time="00:07:56"]]
- **One-story:** $\delta_{e1} = \dfrac{F_1}{K_1}$ (force over story stiffness; combine columns in parallel/series for the equivalent $K$, *Ch 3*).
- **Two-story** (forces $F_1$, $F_2$; stiffnesses $K_1$, $K_2$): $\delta_{e1} = \dfrac{F_1 + F_2}{K_1}$; $\;\delta_{e2} = \delta_{e1} + \dfrac{F_2}{K_2}$.
- **Three-story** (forces $F_1$, $F_2$, $F_3$; stiffnesses $K_1$, $K_2$, $K_3$): $\delta_{e1} = \dfrac{F_1 + F_2 + F_3}{K_1}$; $\;\delta_{e2} = \delta_{e1} + \dfrac{F_2 + F_3}{K_2}$; $\;\delta_{e3} = \delta_{e2} + \dfrac{F_3}{K_3}$.

**Key insight — elastic drift = story shear / story stiffness.** The numerators above are exactly the story shears ($F_1+F_2+F_3 = V_1$, $F_2+F_3 = V_2$, $F_3 = V_3$). So the elastic deflection accumulates from the base up, each level adding $V_x/K_x$: $\;\delta_{e(x)} = \delta_{e(x-1)} + \dfrac{V_x}{K_x}$. The **elastic drift** of a story = $\dfrac{V_x}{K_x}$; it becomes the **code story drift** only after multiplying by $C_d/I_e$. This extends to any number of stories.

### Torsional irregularity exception — compute drift at all corners

Normally the deflection is taken at the **center of mass**.[[cite n="62" video="Chapter 5- P12 ELF- Story Drift" time="00:23:09" page="5-49"]] **EXCEPTION:** for structures in SDC C, D, E, or F with horizontal irregularity **Type 1a (torsional)** or **Type 1b (extreme torsional)**, §12.8.6 requires the story drift $\Delta_x$ to be computed at **all corners** of the structure (the diaphragm rotates under load, so the center-of-mass value is unconservative). Compute the top-minus-bottom deflection at each of the four corners, then use the **largest** as the story drift for that story.

### Story drift check — the allowable $\Delta_a$ and Table 5.11 rows

The calculated (applied) story drift $\Delta_x$ must **not exceed** the maximum allowable story drift $\Delta_a$ from Table 12.12-1 (reproduced as Table 5.11). The allowable depends on the building description and Risk Category (*Ch 4*). Four rows:[[cite n="63" video="Chapter 5- P12 ELF- Story Drift" time="00:27:35" page="5-49"]]

| Row | Description | $\Delta_a$ |
|---|---|---|
| **1** | structures ≤ 4 stories above the base, **other than masonry**, with walls/partitions/ceilings/exterior wall systems designed to accommodate the drift | RC I/II: $0.025\,h_{sx}$ · RC III: $0.020\,h_{sx}$ · RC IV: $0.015\,h_{sx}$ |
| **2** | masonry **cantilever** shear wall structures (any RC) | $0.010\,h_{sx}$ |
| **3** | other masonry shear wall structures (any RC) | $0.007\,h_{sx}$ |
| **4** | all other structures | RC I/II: $0.020\,h_{sx}$ · RC III: $0.015\,h_{sx}$ · RC IV: $0.010\,h_{sx}$ |

($h_{sx}$ = the story height, e.g., 12 ft, 14 ft.)

### Using Row 1 — the three required conditions

Using **Row 1** requires **all three** conditions:[[cite n="64" video="Chapter 5- P12 ELF- Story Drift" time="00:31:21"]] (1) ≤ 4 stories; (2) **not masonry**; (3) the architectural components (interior walls, partitions, ceilings, exterior walls) are **designed to accommodate the story drift**. Condition 3 must be stated **explicitly** in the problem — it **cannot be assumed**. The exam phrases it three equivalent ways: "designed to accommodate the story drift," "flexibly connected to the structure," or "meeting the deformation-compatibility requirements of ASCE 7." If condition 3 is not stated, **drop to Row 4** (for a non-masonry structure).

### Drift as a displacement versus as a ratio

Drift (either $\Delta_x$ or $\Delta_a$) may be expressed as a **displacement** (inches/feet, e.g., $\Delta_x = 2$ in, $\Delta_a = 3$ in) **or** as a **ratio** of the story height (divide by $h_{sx}$, giving e.g., 0.002 or 0.016).[[cite n="65" video="Chapter 5- P12 ELF- Story Drift" time="00:35:20" page="5-49"]] Exam answers are sometimes given as ratios — divide your displacement by the story height to match.

### Additional notes — one-story leeway and the waived period cap for drift

1. A **one-story building** with components designed to accommodate the story drift has **NO drift limit** (no $\Delta_a$ applies) — a code leeway.[[cite n="66" video="Chapter 5- P12 ELF- Story Drift" time="00:37:07" page="5-50"]]
2. If the period $T$ was computed by a **properly substantiated analysis** (rational/Rayleigh, computer model) rather than the approximate $T_a$, then for **drift** calculations the full computed $T$ may be used and the upper-limit cap ($T \le C_u T_a$) is **waived**. The cap $C_u T_a$ applies only when calculating **forces** (base shear, $F_x$), **not** when calculating deflections/drift.

### Additional notes — $\Delta_a/\rho$ for moment-frame systems and deformation compatibility

3. **(Important exam trick)** For SFRS in SDC D, E, or F comprised **solely of moment frames**, the applied drift must satisfy $\Delta_x \le \dfrac{\Delta_a}{\rho}$, where $\rho$ = the redundancy factor (1.0 or 1.3).[[cite n="67" video="Chapter 5- P12 ELF- Story Drift" time="00:41:03"]] Dividing the allowable by $\rho$ (e.g., 1.3) **reduces** it — a **more stringent** requirement. Example: $\Delta_x = 2$ in, table $\Delta_a = 2.5$ in → ordinarily OK, but $2.5/1.3 = 1.92$ in < 2 in → **fails**. The reason: a moment frame is highly redundant but **flexible** (low stiffness, large deflection), so the code penalizes it on drift.
4. **(Conceptual — compatibility of deformations)** For SDC D, E, or F, every structural component **not** part of the SFRS must still be designed to resist the gravity + seismic forces produced by deflecting an amount equal to the story drift, considering **deformation compatibility**. Example: a 3-story, 5-bay frame with a concentrically braced frame (the SFRS) in the middle bay and gravity-only space frames (pinned connections) in the side bays. When the braced frame deflects, the side space frames must deflect with it; they are not part of the SFRS but must be designed for the induced forces. Exams test the **concept**, not the calculation.

### Story drift procedure recap

Drift $\Delta_x = (\delta_{e,\text{top}} - \delta_{e,\text{bottom}})\,\dfrac{C_d}{I_e}$, where $\delta_e$ accumulates from the base up as $\sum (V_x/K_x)$.[[cite n="68" video="Chapter 5- P12 ELF- Story Drift" time="00:52:36"]] Take deflections at the **center of mass** except for torsional/extreme-torsional irregularity in SDC C–F (use the largest of the four corners). Compare the applied $\Delta_x$ against $\Delta_a$ from Table 5.11 (check which row applies; Row 1 needs all three conditions), and for SDC D/E/F moment-frame-only systems use $\Delta_a/\rho$.

### The P-Delta effect — primary and secondary moments

When a structure is subjected to lateral seismic forces ($V \to F_x$), it develops the **primary** moment, shear, and lateral displacement (the story shears, overturning moments, story drift, and deflections computed so far).[[cite n="69" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:00:14" page="5-51"]] In addition, the **column axial loads** — the gravity dead and live load — act on the now-deflected (tilted) configuration, developing an **additional (secondary)** moment, shear, and displacement. This magnification of the member forces and displacements beyond the primary values is the **P-Delta effect**.

### The stability coefficient $\theta$ — definition

For each story, the **stability coefficient**:[[cite n="70" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:04:58" page="5-51"]]

$$\theta = \frac{P \cdot \Delta_x \cdot I_e}{V_x \cdot h_{sx} \cdot C_d}$$

- $P$ = the total **unfactored** vertical load (dead + live) at the **top of the story** under consideration **and all levels above**.
- $\Delta_x$ = the design story drift $= (\delta_{e,\text{top}} - \delta_{e,\text{bottom}})\,C_d/I_e$.
- $I_e$ = importance factor; $V_x$ = story shear; $h_{sx}$ = story height; $C_d$ = deflection amplification factor.

Two-story example: $\theta_2$ uses $P$ = (dead+live at top of story 2 and above), $\Delta_2$, $V_2$, $h_{s2}$; $\theta_1$ uses $P$ = (dead+live at top of story 1 and all above), $\Delta_1$, $V_1$, $h_{s1}$. **Worked summation** (column gravity loads 80, 80 at the level-1 tops and 60, 60 at the level-2 tops in a two-bay frame): for $\theta_1$, $P = 80+80+60+60 = 280$ k (top of story 1 and all above); for $\theta_2$, $P = 60+60 = 120$ k (top of story 2, nothing above).

### Physical meaning of $\theta$ — the secondary/primary moment ratio

$\theta$ is a **ratio of secondary to primary moment**.[[cite n="71" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:12:38" page="5-51"]] Substituting $\Delta_x = (\delta_{e,\text{top}} - \delta_{e,\text{bottom}})\,C_d/I_e$ into the code formula and cancelling $C_d$ and $I_e$ gives the abbreviated form:

$$\theta = \frac{P \cdot (\delta_{e,\text{top}} - \delta_{e,\text{bottom}})}{V_x \cdot h_{sx}}$$

- Numerator $P \cdot (\text{elastic drift}) = P\,\delta$ = the **secondary (additional) moment** from gravity acting on the deflected shape.
- Denominator $V_x \cdot h_{sx}$ = story shear × story height = the **primary overturning moment**.

So $\theta$ = secondary moment / primary moment. $\theta = 10\%$ means the secondary moment is 10% of the primary. Either the full code equation or this fundamental ratio may be used; the exam sometimes tests the concept directly.

### P-Delta Condition 1 ($\theta \le 0.10$) and the $\theta_{max}$ limit

What to do with $\theta$ — three conditions:[[cite n="72" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:19:53" page="5-52"]]

**Condition 1 — $\theta \le 0.10$ (10%):** the P-Delta effect is insignificant and **need not be considered**. Ignore the additional moment/shear/displacement.

**Condition 2 — $0.10 < \theta \le \theta_{max}$:** the P-Delta effect **must be considered**. First, $\theta$ must not exceed

$$\theta_{max} = \frac{0.5}{\beta \cdot C_d} \le 0.25$$

(the secondary moment may never exceed **25%** of the primary). Here $\beta$ = the ratio of the story shear **demand** to the story shear **capacity** (what you designed for ÷ the actual capacity of the as-built columns; e.g., designed for 45 k, capacity 60 k → $\beta = 45/60$). **If $\beta$ is not given, the code conservatively permits $\beta = 1$.**

### P-Delta Condition 2 methods and Condition 3 (redesign)

**Condition 2 is satisfied by one of two methods:**[[cite n="73" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:25:44"]]
- **Method 2A** — a rational / refined / automated **second-order analysis** that explicitly models the deformed (tilted) geometry (first-order uses the upright position; second-order re-analyzes the deflected shape; geometrically nonlinear, done by computer). As an **incentive**, the code relaxes the check from "$\theta \le \theta_{max}$" to "$\dfrac{\theta}{1+\theta} \le \theta_{max}$" (dividing by $1+\theta$ reduces $\theta$).
- **Method 2B (used on the exam)** — **amplify** the computed primary member forces and story drift by the factor $\dfrac{1}{1-\theta}$. Example: $\theta = 0.15$ → $\dfrac{1}{1-0.15} = 1.17$, i.e., increase the bending moment, story shear, and story drift by **17%**. The amplified drift is then checked against $\Delta_a$, and the amplified member forces against the member strength.

**Condition 3 — $\theta > \theta_{max}$:** the structure is too flexible and potentially **unstable** (may collapse / deflect excessively) and **must be redesigned** by increasing stiffness — add a shear wall, a braced frame (concentric or eccentric), or convert to a dual system.

### P-Delta — period cap waived for drift; worst versus best case

For the drift / P-Delta calculation, the upper-limit cap on the period ($T \le C_u T_a$) is **waived** — the full computed (rational) $T$ may be used. The cap applies only when computing **forces**.[[cite n="74" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:35:33"]]

**Theoretical exam question — worst vs best case for P-Delta:** worst case = large $P$ and large $\Delta$ → a **heavy** structure (concrete, masonry) that is also **flexible** (cantilever column, moment frame). Best case = small $P$ and small $\Delta$ → a **light** structure (wood, steel) that is **stiff** (shear wall, braced frame). Exams ask which building is most likely to experience a significant P-Delta effect — pick the **heavy + flexible** one.

### Building separation — $\Delta_{MT}$ and separation from a property line

All buildings/structures on the same property must be separated enough to permit independent seismic displacement **without pounding** (impact) between adjacent structures (§12.12.3).[[cite n="75" video="Chapter 5- P13 ELF- P-Delta, Building Seperation" time="00:41:43" page="5-53"]] When ground motion hits, each building oscillates; an insufficient gap lets them strike one another.

**Required separation $\Delta_{MT}$** between two adjacent buildings (same property):

$$\Delta_{MT} = \sqrt{\Delta_{M1}^2 + \Delta_{M2}^2}$$

— the square root of the sum of the squares of the maximum **inelastic (actual, amplified)** response displacements of building 1 and building 2 computed **at the same height** (where pounding would occur). The displacements are the actual deflections (*the $C_d$ amplification from earlier*): $\Delta_M = \delta_{e,\text{max}}\,C_d/I_e$ (start with the maximum theoretical elastic displacement at the level of interest, then amplify).

**Separation from a property line NOT common to a public way** (a neighbor, not the street): the structure must be set back from the property line by **not less than its own maximum inelastic response displacement** $\Delta_M = \delta_{e,\text{max}}\,C_d/I_e$ (so it does not intrude beyond the line when it deflects).

### Orthogonal interaction — general rule and SDC B/C

**General rule:** seismic design considers the forces in each principal direction **independently** (N-S by itself, E-W by itself — base shear, period, story shear, OTM, drift, one direction at a time).[[cite n="76" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:00:02" page="5-54"]] However, because ground motion can act in any direction, §12.5 requires that for **certain critical elements** the results from both orthogonal directions be **combined** — the **orthogonal interaction** requirement, which depends on the SDC.

- **SDC B** — design for the largest seismic force effect from each principal direction independently. **No orthogonal interaction.**
- **SDC C** — independent, **except** for structures with horizontal irregularity **Type 5 (nonparallel system)**. For Type 5, apply the **100%–30% rule**: 100% of the base shear in one direction acting **concurrently** with 30% of the base shear in the perpendicular direction.
  - **Worked example** (a nonparallel wall receiving forces parallel to itself): 150 k parallel-component from the E-W earthquake and 200 k from the N-S. Try both: $100\%(150) + 30\%(200) = 210$ k; $30\%(150) + 100\%(200) = 245$ k. Design for the larger → **245 k**. (If this same wall were in an SDC B building, there is no interaction — just use the larger single force, 200 k.)

### Orthogonal interaction — SDC D/E/F and the alternative dynamic analysis

**SDC D, E, or F** — independent, **except** for either of two cases, where the 100%–30% rule applies:[[cite n="77" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:11:19" page="5-56"]]
- **(a)** Structures with horizontal irregularity **Type 5 (nonparallel system)**, as in SDC C.
- **(b)** A column or wall that is part of **two or more intersecting SFRS** **and** subjected to an axial force (from seismic in either principal direction) **≥ 20% of the axial design strength** of that column/wall. Example: a **corner column** belongs to the moment frame resisting E-W **and** the one resisting N-S; both directions' $F_x$ produce OTM giving the corner column tension. **Both** conditions must hold.
  - **Worked example** (corner column tension): tension 20 k from N-S, 15 k from E-W, axial force > 20% of capacity. Combine $100\%(\text{larger}) + 30\%(\text{smaller}) = 100\%(20) + 30\%(15) = 24.5$ k (this always governs). Design the column tension for **24.5 k**.

**Alternative to the 100%–30% rule:** for SDC C, D, E, or F, §12.5.3 item (b) permits applying the ground motion in the two principal directions **simultaneously** in a dynamic analysis, in lieu of the 100%–30% rule. (Exams may refer to "§12.5.3 item B" — that is this simultaneous dynamic analysis.)

### Orthogonal interaction summary (Table 5.12)

Summary:[[cite n="78" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:26:44"]]
- **SDC B** → orthogonal interaction neglected.
- **SDC C** → neglected, **except** nonparallel-system (Type 5) irregularity → item A (100%–30% rule) or item B (simultaneous dynamic analysis).
- **SDC D/E/F** → neglected, **except** Type 5 irregularity **or** a column/wall in ≥ 2 intersecting SFRS with axial force ≥ 20% of capacity → item A (100%–30%) or item B.

### ELF limitations — dynamic alternatives; ELF for SDC B/C

ELF is the preferred static procedure.[[cite n="79" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:29:22" page="5-57"]] When it is **not permitted** (ASCE 7 Table 12.6-1, restated as Table 5.13), the alternatives are the two **dynamic** procedures: **modal response spectrum analysis** or **seismic (time) response history analysis** (both always applicable, no limitations). (A fourth path, the **simplified design procedure**, applies only to certain simple structures.)

**Permitted use of ELF:** **SDC B and C** — **all** structures may use ELF (no limitation).

### ELF permitted for SDC D/E/F — the five conditions

**SDC D, E, or F** — ELF is permitted if **any one** of these five conditions holds:[[cite n="80" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:32:39"]]
1. Risk Category I or II **and** not more than two stories above the base.
2. **Light-frame construction** (e.g., wood), any Risk Category, any number of stories.
3. **Regular** structures (no horizontal or vertical irregularity) with structural height **≤ 160 ft**.
4. **Regular** structures with structural height **> 160 ft**, provided $T < 3.5\,T_S$ ($T_S = S_{D1}/S_{DS}$).
5. **Irregular** structures with structural height **≤ 160 ft** that do **NOT** have any of: horizontal Type 1a/1b (torsional/extreme torsional), vertical Type 1a/1b (soft/extreme soft story), Type 2 (weight), or Type 3 (vertical geometric discontinuity).

### ELF not permitted — when a dynamic procedure is required

**ELF NOT permitted** (last row of Table 5.13 — must use a dynamic procedure) for SDC D, E, or F when **either**:[[cite n="81" video="Chapter 5- P14 ELF- Orthogonal Interaction, ELF Limitations" time="00:36:42" page="5-58"]]
- **Condition 1:** structural height > 160 ft **and** $T \ge 3.5\,T_S$ (a tall structure too flexible). (The page-5-58 summary frames the > 160 ft case as: ELF not permitted unless regular **and** $T < 3.5\,T_S$.)
- **Condition 2:** structural height ≤ 160 ft **and** the structure has one or more of the **severe irregularities** — horizontal Type 1a/1b (torsion/extreme torsion), vertical Type 1a/1b (soft/extreme soft story), Type 2 (weight), or Type 3 (vertical geometric discontinuity).

**Which irregularities do NOT bar ELF:** horizontal Type 2 (reentrant corner), horizontal Type 4 (out-of-plane offset), horizontal Type 5 (nonparallel), vertical Type 4 (in-plane discontinuity), and vertical Type 5a/5b (weak/extreme weak story).

### Simplified procedure (§12.14) — eligibility and conditions 1–7

Not every building needs the elaborate ELF procedure. For certain simple bearing-wall and building-frame structures, ASCE 7 **§12.14** provides a **simplified alternative design procedure**, usable in lieu of the other methods provided **all 12 conditions** are met.[[cite n="82" video="Chapter 5- P15 Simplified Design Procedure" time="00:00:43" page="5-58"]] The exam tests conditions **1–4, 11, 12** (5–10 require too much calculation):
1. **Risk Category I or II** (not III or IV).
2. **Site Class A, B, C, or D** (NOT E or F — not soft clay or problematic soil).
3. **Not more than three stories** above grade plane.
4. SFRS is a **bearing wall system OR a building frame system** (a shear wall, CBF, or EBF) — **NOT** a moment frame, dual system, or cantilever column. Use Table 12.14-1.
5. At least **two lines** of lateral resistance in each major axis direction, with at least one on each side of the center of mass.
6. The center of mass in each story is not farther than **10%** of the diaphragm length from the geometric centroid.
7. Eq 12.14-1 (cast-in-place concrete diaphragms with overhangs) or Eq 12.14-2 (all other diaphragms) is satisfied.

### Simplified procedure — conditions 8–12 and when to use it

8. For **rigid diaphragms**, forces are distributed to the vertical SFRS elements as if the diaphragm were **flexible** (per items 8a, 8b).[[cite n="83" video="Chapter 5- P15 Simplified Design Procedure" time="00:04:25"]]
9. Lines of resistance of the SFRS are oriented at angles **≤ 15°** from the major axes.
10. The simplified procedure is used for **each** major orthogonal axis.
11. **No in-plane or out-of-plane offset irregularities** of the SFRS — i.e., NO horizontal Type 4 and NO vertical Type 4. *(Fair exam question.)*
12. The lateral strength of any story **≥ 80%** of the strength of the story above — i.e., NO vertical Type 5a (weak story). *(Fair exam question.)*

Exams may give four buildings and mix/match conditions 1–4, 11, 12 to ask which is eligible for §12.14. Use §12.14 **only** when the problem explicitly says "simplified alternative procedure" or "Article 12.14"; otherwise (if silent) use ELF.

### Determining the SDC and $S_{DS}$ in the simplified procedure

**Determining the SDC:** use Table 5.6 (= IBC Table 1613.5.3.1 / ASCE Table 11.6-1) but only **once**, from the **left column (based on $S_{DS}$ only)** — not twice as in the general procedure — and the Risk Category can only be I or II.[[cite n="84" video="Chapter 5- P15 Simplified Design Procedure" time="00:09:25" page="5-59"]]

**$S_{DS}$ for the simplified procedure:**

$$S_{DS} = \tfrac{2}{3}\,F_a\,S_S$$

- $S_S$ = mapped $\text{MCE}_R$ short-period (0.2 s) spectral acceleration, **except** it need not be taken greater than **1.5** (cap at 1.5).
- $F_a$ = site coefficient, taken simply as **1.0 or 1.4** (NOT from Table 5.2, no interpolation): $F_a = 1.0$ for a **rock** site (≤ 10 ft of soil between the rock and the bottom of the footing); $F_a = 1.4$ for all other soil conditions.

(So this is abbreviated: $S_{DS}$ is **not** read from Table 5.3.)

### Base shear in the simplified procedure ($V = F\,S_{DS}/R \cdot W$)

**Base shear:**[[cite n="85" video="Chapter 5- P15 Simplified Design Procedure" time="00:15:20" page="5-59"]]

$$V = \frac{F \cdot S_{DS}}{R}\,W$$

- $W$ = the effective seismic weight, computed **exactly as for ELF** (dead load of diaphragms + attached walls, plus the applicable service-load portions: 25% storage live load, permanent equipment, 20% snow if > 30 psf, 10 psf office partition minimum, roof gardens/landscaping). No change.
- $S_{DS}$ = the simplified value above.
- $R$ = the response modification coefficient from **Table 12.14-1** (NOT Table 12.2-1). This table has only two categories — A (bearing wall) and B (building frame). Example: special reinforced concrete shear wall — bearing wall $R = 5$; building frame $R = 6$. It also gives system/height limitations by SDC, read like Table 12.2-1: "P" = permitted (no height limit), "NP" = not permitted, a number = max height in feet, and a superscript footnote that permits increasing that height under conditions.
- $F$ = a factor equal to **1.0, 1.1, or 1.2** for buildings that are **one, two, or three** stories above grade plane, respectively.

### Grade plane and stories above grade plane

**"Grade plane"** = the original horizontal ground surface (Figure 5.20).[[cite n="86" video="Chapter 5- P15 Simplified Design Procedure" time="00:22:28" page="5-60"]] Normally a building on horizontal ground has its stories counted above that ground. When part of the building is embedded:
- **(a) Horizontal ground, partially embedded** (Fig 5.20a): a fully embedded story acts like a basement. A story counts as the "first story above grade plane" when the floor surface at the **top** of that story is **more than 6 ft** above the grade plane. Example: a 4-story building with story 1 embedded; if the top-of-story-2 floor is > 6 ft above grade, then story 2 = first story above grade plane, story 3 = second, story 4 = third → three stories above grade plane → $F = 1.2$.
- **(b) Sloped/inclined ground, partially embedded** (Fig 5.20b): compare the floor surface at the top of the story to the **lowest** finished ground level anywhere around the perimeter. The story counts as the first story above grade plane when that floor surface is **more than 12 ft** above the lowest perimeter ground level. (Same example outcome: three stories → $F = 1.2$.)

### Vertical distribution in the simplified procedure

Distribute $V$ by **weight only** (no period-dependent exponent):[[cite n="87" video="Chapter 5- P15 Simplified Design Procedure" time="00:31:39" page="5-59"]]

$$F_x = \frac{w_x}{W}\,V$$

(Compare ELF: $C_{vx} = w_x h_x^{\,k} / \sum w_i h_i^{\,k}$.) Substituting $V = \dfrac{F\,S_{DS}}{R}W$, the total $W$ cancels: $F_x = \dfrac{F\,S_{DS}}{R}\,w_x$.

**Exam point — distribution shape:** in ELF the $F_x$ followed a straight line ($k = 1$) or a parabola ($k \to 2$) depending on the period. Here, since $F_x \propto w_x$, if the story weights are equal ($W_1 = W_2 = W_3$) then $F_1 = F_2 = F_3$ — a **uniform** distribution along the height.

### Drift and building separation in the simplified procedure

**Drift and building separation:**[[cite n="88" video="Chapter 5- P15 Simplified Design Procedure" time="00:38:35" page="5-61"]]
- **Drift limit: NOT checked.** You may compute the applied drift $\Delta_x$, but there is no allowable $\Delta_a$ in the simplified procedure.
- **Building separation / deflection:** instead of force/stiffness, the deflection at level $x$ is taken as **1% of the height** to that level: $\delta_x = 0.01\,h_x$ ($h_x$ = height above the base to level $x$), unless computed to be less. The story drift is taken as **1% of the story height**: $\Delta_x = 0.01\,h_{sx}$.
- The **foundation** must be designed for at least **75%** of the overturning moment at the foundation–soil interface.

### Reducing the seismic base shear — the three techniques

**Starting point: the elastic seismic base shear $V_E$.** From the design response spectrum, the period $T$ gives a spectral acceleration; using it unmodified, $V_E = S_a\,W$.[[cite n="89" video="Chapter 5- P16 Reduction of Base Shear" time="00:00:14"]] Designing for $V_E$ keeps the building elastic, but $V_E$ is very large and uneconomical. To reduce the design base shear $V$, the **design spectral acceleration must be reduced**. Three techniques:
1. **Allow inelastic predetermined damage** (the code approach).
2. **Seismic base isolation.**
3. **Damping systems.**

### Technique 1 — inelastic predetermined damage (plastic hinges)

Conventional codes allow design force levels **below** the elastic level by accepting localized inelastic behavior.[[cite n="90" video="Chapter 5- P16 Reduction of Base Shear" time="00:04:08"]] Take $V_E$, divide by $R$ and multiply by $I_e$: $\;V = V_E\,\dfrac{I_e}{R}$. The building yields (responds inelastically) at this reduced force — the hysteresis behavior. Damage is accepted at **predetermined locations** well-designed, well-detailed, and well-constructed to dissipate the energy without collapse. These are **plastic hinges**:
- **Shear wall** → plastic hinge at the **base** of the wall (above the footing).
- **Moment frame** → plastic hinges at the **beam ends**, near the connection to the column.

This localized inelastic behavior dissipates energy and reduces the force level — the purpose of $R$.

### Technique 2 — seismic base isolation and how it reduces base shear

The building is jacked up, cut from its footings, and **isolators** are installed (rollers, lead-rubber bearings, friction pendulums).[[cite n="91" video="Chapter 5- P16 Reduction of Base Shear" time="00:09:03" page="5-62"]] Under ground motion the building translates on the isolators with little damage to the structure itself; the energy is dissipated at the isolation layer through shear deformation. The isolator reduces horizontal acceleration while still carrying the gravity load to the foundation.

**How it reduces base shear:** seismic isolation **increases the natural period** of the building. On the response spectrum (*Ch 3*), a longer period gives a **smaller spectral acceleration**, so $S_a\,W$ (the base shear) is reduced.

### When base isolation is effective (and when detrimental)

A frequent exam question:[[cite n="92" video="Chapter 5- P16 Reduction of Base Shear" time="00:14:06"]]
- **Recommended:** a **stiff / short-period** structure founded on **rock**. (Short period attracts the largest acceleration; lengthening it gives a big reduction — the best use of isolation.)
- **Not recommended / can be detrimental:** a **flexible / tall** structure on **soft soil** (bay mud). The structure already has a long period; isolation lengthens it further, giving little reduction, and may cause **resonance** — the long-period structure, the long-period soft soil, and the long-period Rayleigh/surface waves can have coinciding periods (≈ 2 s each), which is catastrophic and may **increase** the seismic demand (*the Mexico City 1985 resonance from Ch 2*).

### Technique 3 — damping systems

**Passive energy-dissipation devices (dampers)** — like a car's shock absorbers — are installed, typically on diagonal braces.[[cite n="93" video="Chapter 5- P16 Reduction of Base Shear" time="00:19:17"]] They reduce the structure's acceleration response and base shear by **increasing the damping ratio**. Instead of the typical 5% damping, the building may reach **15–20% or more**. (*Ch 3: for a given period, a higher damping ratio $\beta$ gives a smaller spectral acceleration.*) Types: viscous, viscoelastic, friction, and yielding-metallic dampers. Used in new buildings and in the **seismic retrofit** of existing buildings (add braces + dampers to steel frames); the dampers take the beating during the earthquake.

### Summary — the three base-shear-reduction techniques

All three reduce the base shear **by reducing the spectral acceleration**:[[cite n="94" video="Chapter 5- P16 Reduction of Base Shear" time="00:23:01"]]
- **Inelastic predetermined damage** (code): divide $V_E$ by $R$ → accept hysteresis at plastic hinges (shear-wall base, beam ends).
- **Base isolation:** increase the natural period → lower $S_a$ (best for stiff structures on rock; risky for flexible structures on soft soil due to resonance).
- **Damping systems:** increase the damping ratio $\beta$ → lower $S_a$.

### Seismic load effect $E$ — internal loads; horizontal and vertical effects

$E$ = the **earthquake load** = the **internal loads** (axial force, shear force, bending moment) developed in the structure from the earthquake-induced forces — exactly the $V$, $OTM$, axial forces, etc. obtained from the ELF procedure.[[cite n="95" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:01:16" page="5-63"]] $E$ must be computed by applying both the **horizontal AND vertical** seismic forces. For certain critical elements the effect is also modified by the overstrength factor $\Omega_0$ (a special case). Total effect:

$$E = E_h \pm E_v$$

where $E_h$ = the **horizontal** seismic load effect and $E_v$ = the **vertical** seismic load effect.

### Combining $E_h$ and $E_v$ (additive versus counteracting gravity)

Combining (Figure 5.21):[[cite n="96" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:06:03" page="5-63"]]
- $E = E_h + E_v$ (both positive) — when the seismic effect is **additive** to gravity, giving the **maximum** gravity effect.
- $E = -E_h - E_v$ (both negative) — when the seismic effect **counteracts** gravity, giving the **minimum** gravity effect.

**Example** (two-story column under gravity dead-load compression):
- **Right column:** dead-load compression 50 k + earthquake compression 30 k (same direction) → use $+E_h+E_v$ → **maximum axial compression = 80 k**.
- **Left column:** dead-load compression 50 k, earthquake 30 k opposite → use $-E_h-E_v$ → **minimum axial compression = $50 - 30 = 20$ k**.
- If the earthquake effect is larger (60 k) and opposes gravity: left column → $50 - 60 = -10$ k → **maximum axial tension (uplift)**.

The positive equation gives max compression; the negative gives min compression or max tension.

### Horizontal seismic load effect $E_h = \rho\,Q_E$

The horizontal seismic load effect:[[cite n="97" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:16:47" page="5-64"]]

$$E_h = \rho \cdot Q_E$$

- $Q_E$ = the internal seismic load (axial, shear, bending moment) from the horizontal seismic forces — the $V$/$M$/$P$ from the ELF analysis, relabeled $Q_E$.
- $\rho$ = the **redundancy factor**. Because the earthquake direction is arbitrary, $E_h = \rho(\pm Q_E)$ — taken with both a positive and a negative sign.

### The redundancy factor $\rho$ (1.0 or 1.3)

$\rho$ indicates whether the seismic load is resisted by an **adequate number** of vertical SFRS elements creating **multiple paths of resistance**.[[cite n="98" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:18:56" page="5-64"]] $\rho$ is either **1.0 or 1.3**.
- **Example** (Fig 5.22): a building with **five** moment frames resisting N-S is highly redundant — if one frame yields (plastic hinges at both beam ends), four remain to redistribute → $\rho = 1.0$. A building with only **two** moment frames lacks redundancy → $\rho = 1.3$.
- $\rho = 1.3$ is a **penalty**: multiply the demands ($Q_E$ = shear, moment, axial) by 1.3 (a 30% increase) for less-redundant systems.
- $\rho$ is calculated for **each SFRS in each orthogonal direction independently** (the N-S $\rho$ may differ from the E-W $\rho$).

($\rho$ was used earlier — the two-stage analysis force transfer, and the allowable drift $\Delta_a/\rho$ for moment-frame-only systems — but not defined until now.)

### When $\rho = 1.0$ — the nine conditions

$\rho = 1.0$ when **any one** applies:[[cite n="99" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:35:30" page="5-64"]]
1. **SDC B or C.**
2. **Drift and P-Delta** calculations (displacements, not forces).
3. Non-structural components designed with $F_p$ (architectural/mechanical/electrical, Chapter 7).
4. Non-building structures **not** similar to buildings (tanks, hoppers, silos — Chapter 8).
5. Collector elements, splices, and connections designed with the overstrength factor $\Omega_0$.
6. Members and connections where the overstrength ($\Omega_0$) load combinations are required.
7. Diaphragm loads ($F_{px}$ — the floor diaphragm, Chapter 6).
8. Structures with **damping systems**.
9. Structural walls for **out-of-plane** seismic forces, including their anchorage (Chapter 7).

(For 5 and 6: critical elements like collectors are designed with $\Omega_0$ — amplifying forces 100–200% — so they stay elastic; since $\Omega_0$ already governs, $\rho = 1.0$.)

### $\rho = 1.3$ default for SDC D/E/F; relaxing via the >35% story rule

For **SDC D, E, or F**, $\rho = 1.3$ by **default**.[[cite n="100" video="Chapter 5- P17 Seismic Load Effects - 1" time="00:42:05" page="5-65"]] It may be relaxed to $\rho = 1.0$ if **either** condition is met.

**Condition 1** (Table 5.14 / ASCE Table 12.3-3): for each story resisting **more than 35%** of the base shear, the structure complies with the table. **"Story resisting > 35%"** example (3-story, $F = 5/16/9$ k → story shears $V_3 = 9$, $V_2 = 25$, $V_1 = 30$; base shear = 30 k): $V_3/V = 9/30 = 30\%$ (< 35% → ignore); $V_2/V = 25/30 \approx 83\%$; $V_1/V = 30/30 = 100\%$ — so only stories 1 and 2 must satisfy the table. The table conditions:
- **Moment frame:** loss of moment resistance at both ends of a single beam would not reduce the story strength by more than **33%**. (Five frames → lose one → $1/5 = 20\% < 33\%$ → OK → $\rho = 1.0$. Two frames → lose one → $1/2 = 50\% > 33\%$ → cannot relax → $\rho = 1.3$.)
- **Braced frame:** removal of an individual brace or its connection would not reduce the story strength by more than **33%**. (Four braces → lose one → $1/4 = 25\% < 33\%$ → OK.)
- **Shear walls / wall piers / cantilever columns:** same methodology.

### Relaxing $\rho$ — Condition 2 (perimeter bays) and counting bays

**Condition 2** (Fig 5.23): the structure has **no plan irregularities** **and** the SFRS has at least **two bays of perimeter SFRS on each side** of the structure in the considered direction, at each story resisting > 35% of the base shear.[[cite n="101" video="Chapter 5- P17 Seismic Load Effects - 1" time="01:00:28" page="5-65"]] (A "bay" = column-beam-column for moment/braced frames.) Counting bays for a **shear wall** depends on the material:
- **Masonry, concrete, or steel-plate wall:** number of equivalent bays = $\dfrac{L}{h_s}$ (total wall length / story height).
- **Light-frame shear wall** (wood structural panel or gypsum wallboard): number of bays = $\dfrac{2L}{h_s}$.

### Vertical seismic load effect $E_v = 0.2\,S_{DS}\,D$

Rather than applying actual vertical seismic forces (complex), most codes ignore them and use a fraction of the dead load:[[cite n="102" video="Chapter 5- P17 Seismic Load Effects - 1" time="01:25:43" page="5-66"]]

$$E_v = 0.2\,S_{DS}\,D$$

where $D$ = the dead-load axial force / shear / moment and $S_{DS}$ = the design short-period spectral acceleration. Because vertical ground motion is arbitrary, $E_v = \pm 0.2\,S_{DS}\,D$ (take the sign that produces the desired effect; combine as $+E_h+E_v$ or $-E_h-E_v$).

$E_v$ may be taken as **zero** when either: (a) **SDC B** — design only for $E_h$; or (b) determining demands at the soil-structure interface of the foundation (beyond this exam's level).

### Horizontal cantilever members — minimum net upward force

**Special case — horizontal cantilever members:** horizontal cantilevers (balconies) in structures in SDC D, E, or F must be designed for a minimum **net upward force of $0.2\,D$** (applied by itself, pushing upward), in addition to all other applicable downward seismic load effects ($E_h$, $E_v$).[[cite n="103" video="Chapter 5- P17 Seismic Load Effects - 1" time="01:31:33" page="5-68"]]

### Seismic load effect with the overstrength factor $E_m$ — what it is for

Formerly the "special" seismic load effect; now the **seismic load effect with the overstrength factor**, $E_m$ (distinct from the ordinary $E = E_h + E_v$).[[cite n="104" video="Chapter 5- P18 Seismic Load Effects - 2" time="00:00:02" page="5-68"]] Used for certain **critical elements** of the SFRS — e.g., a **collector** that transfers force from a second-story shear wall offset above a first-story shear wall (vertical Type 4 irregularity). If the collector yields, the load cannot transfer between the two walls, so such elements must stay **elastic**; they are designed for the overstrength factor $\Omega_0$ (Table 12.2-1) instead of $\rho$. (Exactly when $\Omega_0$ must be applied is covered at the end of the chapter.)

### $E_m = E_{mh} \pm E_v$ (with $E_{mh} = \Omega_0\,Q_E$); $E$ versus $E_m$

The overstrength seismic load effect:[[cite n="105" video="Chapter 5- P18 Seismic Load Effects - 2" time="00:02:41"]]

$$E_m = E_{mh} \pm E_v$$

- $E_{mh} = \Omega_0 \cdot Q_E$ — the maximum horizontal effect ($\rho$ is **replaced** by $\Omega_0$, which is 2, 2.5, or 3 — much larger than $\rho = 1.3$). $Q_E$ = the axial/shear/moment from the analysis.
- $E_v = 0.2\,S_{DS}\,D$ — the vertical effect, **unchanged** from the ordinary case (no "M" subscript, since it is identical).
- $E_m$ is also called the **maximum seismic load effect** (the maximum seismic force that can develop in an element).

Combining (same logic as the ordinary $E$):
- $E_m = E_{mh} + E_v$ (positive) — earthquake **additive** to gravity → maximum compression.
- $E_m = -E_{mh} - E_v$ (negative) — earthquake **counteracts** gravity → minimum compression or maximum tension.

The **only** difference between $E_m$ and $E$ is that the horizontal term uses $\Omega_0\,Q_E$ ($E_{mh}$) instead of $\rho\,Q_E$ ($E_h$). The vertical term and the ± sign convention are identical.

### Load combinations — load symbols and the three basic sets

Having quantified the seismic load effects ($E_h$, $E_v$, and the overstrength $E_m$), we now combine them with the other loads (*the permitted design methods / limit states from Ch 4*).[[cite n="106" video="Chapter 5- P19 Load Combinations, Games" time="00:00:01" page="5-69"]]

**Load symbols:** $D$ = dead, $E$ = seismic load effect ($E_m$ = with overstrength $\Omega_0$), $F$ = fluid, $H$ = earth/groundwater pressure, $L$ = live (except roof), $L_r$ = roof live, $R$ = rain, $S$ = snow.

**Three basic load combinations** (plus the special overstrength combination):
- **Basic Strength Design (SD) / LRFD** — from ASCE 7.
- **Basic Allowable Stress Design (ASD)** — from ASCE 7.
- **Alternative Basic ASD** — a legacy set, in **IBC only** (not in ASCE 7).

IBC gives only the headers and refers to ASCE 7 for the equations. In each set, only certain equations include $E$. Every set has a **maximum-effect** equation (seismic additive to gravity) and a **minimum-effect** equation (seismic opposes gravity). The word "gravity" is dropped → "maximum effect" and "minimum effect."

### Strength Design / LRFD combinations (maximum and minimum effect)

**Strength Design / LRFD** (ASCE 7; 7 combinations, 2 include $E$):[[cite n="107" video="Chapter 5- P19 Load Combinations, Games" time="00:03:37" page="5-69"]]
- **Maximum effect (Eq 6):** $(1.2 + 0.2\,S_{DS})\,D + F + \rho\,Q_E + f_1 L + f_2 H + 0.2\,S$ [E expanded as $+E_h + E_v$]
- **Minimum effect (Eq 7):** $(0.9 - 0.2\,S_{DS})\,D + F + \rho\,Q_E + f_2 H$ [E expanded as $-E_h - E_v$]

**Factors:** $f_1$ (on $L$) = 1.0 for public assembly with $L > 100$ psf and for parking garages, else 0.5. $f_2$ (on $H$) = 1.6 if $H$ adds to the principal loads; 0.9 if $H$ resists and is permanent; 0 if $H$ resists but is not permanent.

### Allowable Stress Design (ASD) combinations

**Allowable Stress Design (ASD)** (ASCE 7; 10 combinations, 3 include $E$):[[cite n="108" video="Chapter 5- P19 Load Combinations, Games" time="00:20:36" page="5-70"]]
- **Maximum effect (Eq 8):** $(1.0 + 0.14\,S_{DS})\,D + f_3 H + F + 0.7\,\rho\,Q_E$
- **Maximum effect (Eq 9):** $(1.0 + 0.105\,S_{DS})\,D + f_3 H + F + 0.75 \cdot 0.7\,\rho\,Q_E + 0.75\,L + 0.75\,S$
  ($0.14 = 0.7 \times 0.2$; $0.105 = 0.75 \times 0.7 \times 0.2$.)
- **Minimum effect (Eq 10):** $(0.6 - 0.14\,S_{DS})\,D + F + 0.7\,\rho\,Q_E + f_3 H$

**Factor $f_3$** (on $H$) = 1.0 if $H$ adds to the principal loads; 0.6 if $H$ resists and is permanent; 0 if $H$ resists but is not permanent.

### Alternative Basic ASD combinations

**Alternative Basic ASD** (IBC only; 6 combinations, 2 include $E$):[[cite n="109" video="Chapter 5- P19 Load Combinations, Games" time="00:30:55" page="5-71"]]
- **Maximum effect (IBC 16-11):** $(1.0 + 0.14\,S_{DS})\,D + \dfrac{\rho\,Q_E}{1.4} + L + S$ (dividing $E$ by 1.4 ≡ multiplying by ~0.7, so $0.7 \times 0.2 = 0.14$).
- **Minimum effect:** $(0.9 - 0.14\,S_{DS})\,D + \dfrac{\rho\,Q_E}{1.4}$.

### The special overstrength load combination

The **special overstrength load combination** is identical to the SD/LRFD and ASD equations above **except $\rho\,Q_E$ is replaced by $\Omega_0\,Q_E$ ($E_{mh}$)**.[[cite n="110" video="Chapter 5- P19 Load Combinations, Games" time="00:37:34" page="5-72"]] The vertical term $0.2\,S_{DS}\,D$ and all other factors are unchanged.
- **SD/LRFD maximum:** $(1.2 + 0.2\,S_{DS})\,D + 1.2\,F + \Omega_0\,Q_E + f_1 L + f_2 H + 0.2\,S$
- **SD/LRFD minimum:** $(0.9 - 0.2\,S_{DS})\,D + 0.9\,F + \Omega_0\,Q_E + f_2 H$
- **ASD maximum:** $(1.0 + 0.14\,S_{DS})\,D + f_3 H + F + 0.7\,\Omega_0\,Q_E$ (and the 0.105 companion)
- **ASD minimum:** $(0.6 - 0.14\,S_{DS})\,D + 0.6\,F + 0.7\,\Omega_0\,Q_E + f_3 H$

### Sign-convention rules for $Q_E$ and the vertical term

Critical sign rules (both apply to $Q_E$ and the $0.2\,S_{DS}\,D$ vertical term):[[cite n="111" video="Chapter 5- P19 Load Combinations, Games" time="00:16:13"]]
- **Maximum effect:** $Q_E$ takes the **same sign as $D$** (single asterisk in the book). If $D$ is +, $Q_E$ is +; if $D$ is −, $Q_E$ is −. The vertical term is **added** ($+0.2\,S_{DS}\,D$).
- **Minimum effect:** $Q_E$ takes the **opposite sign to $D$** (double asterisk). The vertical term is **subtracted** ($-0.2\,S_{DS}\,D$).

The sign of $D$ is fixed; $Q_E$ is the term that flips. ($Q_E$ can be axial, shear, or moment and is inherently ±.)

### Choosing maximum versus minimum effect (look at gravity first)

How to choose max vs min — look at **gravity (the dead load) first**, not the words "maximum/minimum":[[cite n="112" video="Chapter 5- P19 Load Combinations, Games" time="00:50:38"]]
- Dead load gives tension **and** the question wants maximum tension → going **with** gravity → **maximum effect**.
- Dead load gives compression **and** the question wants maximum tension → going **against** gravity → **minimum effect**.

**Pointers:** the axial load in a column from gravity/dead load is **always compression** (the weight of the structure). Bending moment and shear from dead load can be + or −. $Q_E$ (axial, shear, moment) can be + or − depending on earthquake direction.

### When the overstrength ($\Omega_0$) combination is required — the four triggers and the wood exception

The **four triggering conditions**:[[cite n="113" video="Chapter 5- P19 Load Combinations, Games" time="00:43:54" page="5-73"]]
1. **Horizontal irregularity Type 4** (out-of-plane offset).
2. **Vertical irregularity Type 4** (in-plane discontinuity).
3. The **foundation** providing overturning resistance at the base of a **cantilever column**.
4. **Collector elements** and their connections in SDC C, D, E, or F.

**Exception:** the overstrength combination is **NOT required** for collector elements/connections in structures braced **entirely by light-frame wood shear walls** — use $\rho$ (the basic combination) instead. So if (4) were a **wood** structure, the answer would be **no**.
