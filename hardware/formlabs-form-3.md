# Formlabs Form 3 resin printer

> **Read this when** you are about to print on the lab's Formlabs Form 3, handle its resin or isopropyl alcohol, or maintain the printer.

This page covers the Form 3 resin 3D printer: its specs, how a print goes from PreForm to a washed and cured part, compatible resins, maintenance and, above all, how to handle resin and solvent safely and dispose of them through Kent State University's Environmental Health and Safety office. The one thing to remember: **liquid resin and used isopropyl alcohol are chemical waste**. Wear gloves and eye protection, and never pour either into a drain or the trash.

## Contents

- [Overview](#overview)
- [Key specs](#key-specs)
- [In our lab](#in-our-lab)
- [First steps](#first-steps)
- [Software](#software)
- [Safety](#safety)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)
- [Related](#related)

## Overview

The [Formlabs Form 3](https://formlabs.com/3d-printers/form-3/) is a desktop stereolithography (SLA) printer: a laser cures liquid photopolymer resin layer by layer into a solid part. Formlabs calls its method Low Force Stereolithography (LFS): a flexible-film resin tank and a Light Processing Unit (LPU) that holds the laser and optics. Resin parts are smoother and more detailed than parts from a filament (FDM) printer, but they need washing in isopropyl alcohol (IPA) and curing under light and heat after printing.

What the lab uses it for: `[what the lab prints on the Form 3, for example prototype parts and robot fixtures]`. Who may use it: `[trained users]`. Resin costs money, so prints need `[resin budget/approval]`.

> [!NOTE]
> Formlabs has replaced the Form 3 line with the Form 4. Its [support notice](https://formlabs.com/support/Ongoing-support-for-the-Form-3-and-Form-3B/) says consumables and support for Form 3 generation printers continue "until at least January 2028", and spare parts until at least January 2027.

## Key specs

From the Form 3 column of Formlabs' [resin printer tech specs](https://formlabs.com/3d-printers/resin/tech-specs/), checked Sept. 30, 2026.

| Spec | Form 3 |
| --- | --- |
| Technology | Laser stereolithography (SLA), Low Force Stereolithography (LFS) |
| Light source | One Light Processing Unit: Class 1 laser product, 405 nm, 250 mW laser, 85 µm laser spot |
| Build volume | 14.5 × 14.5 × 19.3 cm (4.05 L) |
| Layer thickness | 25-300 µm |
| XY resolution | 25 µm |
| Resin heating | Heats resin to 35 °C |
| File input | STL, OBJ and 3MF (PreForm writes FORM files) |
| Connectivity | Wi-Fi (2.4 and 5 GHz), Ethernet (1000 Mbit), USB-B 2.0 |
| Printer size | 40.5 × 37.5 × 53 cm; minimum access space 40.5 × 53 × 78 cm (for opening the cover) |
| Weight | 17.5 kg |
| Operating environment | 18 °C to 28 °C |
| Power | 100-240 VAC, 2.5 A, 50/60 Hz, 220 W |
| Resin tank lifetime | 250-800 hours of printing and/or 10-35 weeks exposed to resin, depending on material |

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Location | `[Room ###, the printer's station]` |
| Owner or contact | `[Form 3 owner or contact name]` |
| Who may print | `[trained users]` (trained by `[Form 3 trainer name]`) |
| Booking and checkout | `[procedure for booking the printer]` |
| Resin budget and approval | `[resin budget/approval]` |
| Resins and tanks on hand | `[resins, resin tank versions]` |
| Post-processing | `[Form Wash and Form Cure models, or other wash and cure setup]` |
| Chemical waste | `[lab resin and IPA waste procedure]`, including who requests EHS pickups |
| Accounts and credentials | PreForm and Dashboard sign-in: ask `[lab manager name]` for the lab's Formlabs account; never commit it to any repo |

## First steps

Your first prints are with `[Form 3 trainer name]`. The workflow, from Formlabs' support pages:

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware) and read [Safety](#safety) below, including the resin safety data sheet (SDS) for the resin you will use.
2. **Prepare the file in PreForm** (free, [download](https://formlabs.com/software/preform/)): import an STL, OBJ or 3MF file, choose the printer and the resin that is loaded, then orient the part, add supports and check the layout.
3. **Check the printer** before you send the job: the cartridge and tank match the resin in PreForm, the tank is inspected and has no cured debris, the build platform is clean and seated and the cover closes.
4. **Send the print** over Wi-Fi, Ethernet or USB and start it from the touchscreen.
5. **Remove the part** wearing nitrile or neoprene gloves and safety glasses. Keep resin off the touchscreen and outside surfaces.
6. **Wash** in IPA of 90% concentration or higher ([IPA guide](https://formlabs.com/support/Isopropyl-Alcohol-IPA/)) for the time your resin needs, for example 10 minutes for Grey, Black, Clear or White Resin V4 ([wash times](https://formlabs.com/support/Form-Wash-Time-Settings/)). Let the parts dry.
7. **Remove supports** and **post-cure** at the time and temperature Formlabs lists for your resin ([cure settings](https://formlabs.com/support/Form-Cure-Time-and-Temperature-Settings/)).
8. **Clean up:** wipe spills with paper towels while wearing gloves, put resin-soaked towels and gloves in the resin waste container (`[lab resin and IPA waste procedure]`) and log the print in `[print log]`.

## Software

| Software or resource | What it is | Link |
| --- | --- | --- |
| PreForm | Free print-preparation software: orientation, supports, layout, printer management. Windows 10 (64-bit, version 1809 or later) and macOS 13 or later | [PreForm](https://formlabs.com/software/preform/) |
| Dashboard | Formlabs' web service to follow prints and track resin, tanks and service coverage | [Dashboard](https://formlabs.com/software/dashboard/) |
| Printer firmware | Form 3/Form 3+ firmware 2.5.6 (March 24, 2026); update through PreForm | [Release notes](https://formlabs.com/support/Firmware-Release-Notes/), [how to update](https://formlabs.com/support/Updating-firmware-SLA/) |
| Materials library | Every Formlabs resin with its compatible printers and tanks | [Materials](https://formlabs.com/materials/), [choosing a material](https://formlabs.com/support/Choosing-the-Right-Material/) |
| Safety and technical data sheets | SDS and technical data sheet for each resin | [Data sheets](https://formlabs.com/materials/data-sheets/) |

**Resins.** Formlabs' [material guide](https://formlabs.com/support/Choosing-the-Right-Material/) lists which resins print on the Form 3: general-purpose resins (such as Grey, Black, White, Clear, Draft and Model) and engineering resins (such as Tough 1500, Tough 2000, Durable, Rigid 4000, Flexible 80A and High Temp), among others. Some newer resins are Form 4 only, and BioMed and dental resins need the Form 3B. Check the guide before you order.

**Resin tanks.** Resin Tank V2.1 prints "all resins compatible with the Form 3/Form 3+"; the older V1 tank can't be used with several resins, including Rigid 4000, Tough 2000 and Grey Pro ([tank types](https://formlabs.com/support/Understanding-the-different-types-of-resin-tanks-Form-3/)). Formlabs says to "use a different resin tank for each type of Formlabs resin" ([resin care](https://formlabs.com/support/Resin-Care/)).

### Maintenance

From Formlabs' [maintenance schedule](https://formlabs.com/support/Schedule-of-maintenance-Form-3/) and related articles. Maintenance is done by `[who maintains the printer]`.

- **Optical window (on the LPU), monthly.** Inspect it and remove dust with a dry PEC*PAD wipe and a rubber bulb blower. "Minimal cleaning is the best cleaning"; avoid compressed air, and use only 90% or higher IPA if a wet wipe is needed ([cleaning the optical window](https://formlabs.com/support/Cleaning-the-Glass-Optical-Window-Form3/)). Keep the cover closed when the printer is idle.
- **Resin tank.** Inspect and clean it after a failed print, and "do not use sharp or metal tools in the resin tank" ([tank inspection](https://formlabs.com/support/Inspecting-and-cleaning-resin-tanks-Form-3/)). Replace it at the end of its life: "Using a resin tank beyond its life expectancy greatly increases the risk of a resin spill" ([tank lifetime](https://formlabs.com/support/Resin-tank-lifetime-Form-3-Form-3B/)).
- **IPA.** Replace the wash IPA when resin reaches about 10% of it, which the Form Wash hydrometer shows ([replacing IPA](https://formlabs.com/support/Replacing-IPA/)).
- **Firmware and PreForm.** Check for updates monthly.
- **Placement.** Keep the printer on a stable, level surface in an 18-28 °C room ([Form 3 manual, via manuals page](https://formlabs.com/support/Manuals-and-documentation/)).

## Safety

Read the lab's [3D printing and resin rules](../lab-rules/safety.md#3d-printing-and-resin) and the resin's safety data sheet first. The rules below are Formlabs' guidance from [Safety with Formlabs SLA printers](https://formlabs.com/support/Safety-Formlabs-SLA-printers/), [resin care](https://formlabs.com/support/Resin-Care/) and [disposing of resin](https://formlabs.com/support/Disposing-of-resin/), plus Kent State's waste rules.

> [!WARNING]
> **Protect your skin and eyes.** Formlabs warns that skin contact "may cause an allergic skin reaction" and eye contact may cause irritation. "Always wear non-reactive nitrile or neoprene gloves" (not latex) when you handle liquid resin, printer parts, unwashed prints or solvent, and wear safety glasses, "particularly during post-processing". If resin touches your skin, wash it with soap and water; Formlabs says not to use hand sanitizer or other alcohol on skin. In an emergency, "refer to the safety data sheet and seek help", and report it as the lab's [injury reporting rules](../lab-rules/safety.md#reporting-injuries-and-hazards) say.

- **Ventilation.** Formlabs recommends a room with at least three full air exchanges per hour and says printers "should not be operated in closed off, unventilated spaces" such as closets.
- **Food.** "Do not eat, drink, or smoke in the printing work area."
- **Resin storage.** Store resin in its closed cartridge at 10-25 °C, away from sunlight. "Do not pour resin back into cartridges."
- **Safety data sheets.** Find the SDS for each resin on Formlabs' [data sheets page](https://formlabs.com/materials/data-sheets/), and keep a copy where the lab keeps its chemical records: `[SDS location]`. Kent State tracks academic lab chemicals in its CEMS system ([Kent State safety data sheets](https://www.kent.edu/facilitiesplanning/safety-data-sheets)).
- **Laser.** The Form 3 is certified as a Class 1 laser product. Don't open the Light Processing Unit or modify the printer.

> [!CAUTION]
> **Isopropyl alcohol is flammable.** Use and store IPA "away from ignition sources", in a well-ventilated area, and keep small quantities "in appropriately labeled and sealed containers" ([IPA guide](https://formlabs.com/support/Isopropyl-Alcohol-IPA/)).

### Waste disposal through Kent State EHS

Formlabs says uncured resin "may be classified as hazardous waste" and that you should "add it to your chemical waste stream in accordance with all applicable regulations"; it also says to "never pour solvent that contains dissolved resin into drains" ([used solvent](https://formlabs.com/support/How-can-I-dispose-of-resin-and-used-solvent/)). At Kent State, that stream runs through **Environmental Health and Safety (EHS)**:

| Waste | What to do |
| --- | --- |
| Liquid or partly cured resin, resin-soaked towels and gloves | Collect in the lab's labeled resin waste container for EHS pickup: `[lab resin and IPA waste procedure]` |
| Used IPA with dissolved resin | Collect in a closed, labeled container for EHS pickup. Never pour it down a drain |
| Fully washed and cured parts and supports | Formlabs lists them as household waste, and the lab's [resin rules](../lab-rules/safety.md#3d-printing-and-resin) allow the regular trash |
| Empty cartridges and failed tanks | Ask `[lab manager name]`; don't throw away a cartridge or tank that still holds liquid resin |

- Kent State's waste management page says to "contact the Environmental Health and Safety Office at 330-672-1950" to arrange hazardous waste disposal, and that containers "must be labeled or marked so that their contents are known" ([waste management services](https://www.kent.edu/universityarchitect/waste-management-services)).
- For other questions, EHS is at 330-672-4347 or <ehs@kent.edu> ([Environmental Health and Safety](https://www.kent.edu/facilitiesplanning/environmental-health-and-safety)).
- EHS offers a "Lab Safety: Hazardous Waste Guide" course ([EHS training](https://www.kent.edu/facilitiesplanning/training)). Which EHS courses Form 3 users must complete: `[required EHS trainings]`.
- Formlabs also describes curing leftover resin in sunlight before disposal when no chemical waste stream exists. The lab has one, so use EHS.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| Parts come off the build platform | Follow Formlabs' non-adherence checklist (platform, tank, supports, orientation) | [Non-adherence](https://formlabs.com/support/Non-Adherence/) |
| Layers separate from one another | Follow the delamination guide | [Delamination](https://formlabs.com/support/Delamination/) |
| Prints fail after they printed well before | Contamination on the optical window can weaken the laser: inspect and clean it | [Cleaning the optical window](https://formlabs.com/support/Cleaning-the-Glass-Optical-Window-Form3/) |
| A print failed and left debris in the tank | Clean the tank before the next print, without metal tools | [Cleaning after a failed print](https://formlabs.com/support/Cleaning-After-a-Failed-Print-Form3/) |
| An error message on the touchscreen | Look it up in Formlabs' error list, then tell `[Form 3 owner or contact name]` | [Form 3 error messages](https://formlabs.com/support/Form-3-error-messages/) |
| Resin temperature warnings | Check the room temperature (18-28 °C) and the resin heating guidance | [Maintaining resin temperature](https://formlabs.com/support/Maintaining-Resin-Temperature/) |

## Resources

- Formlabs: [Form 3](https://formlabs.com/3d-printers/form-3/) · [tech specs](https://formlabs.com/3d-printers/resin/tech-specs/) · [PreForm](https://formlabs.com/software/preform/) · [manuals](https://formlabs.com/support/Manuals-and-documentation/) · [maintenance schedule](https://formlabs.com/support/Schedule-of-maintenance-Form-3/) · [safety](https://formlabs.com/support/Safety-Formlabs-SLA-printers/) · [resin care](https://formlabs.com/support/Resin-Care/) · [disposing of resin](https://formlabs.com/support/Disposing-of-resin/) · [data sheets](https://formlabs.com/materials/data-sheets/) · [support notice for the Form 3](https://formlabs.com/support/Ongoing-support-for-the-Form-3-and-Form-3B/)
- Kent State: [Environmental Health and Safety](https://www.kent.edu/facilitiesplanning/environmental-health-and-safety) · [waste management services](https://www.kent.edu/universityarchitect/waste-management-services) · [EHS training](https://www.kent.edu/facilitiesplanning/training) · [safety data sheets (CEMS)](https://www.kent.edu/facilitiesplanning/safety-data-sheets)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [SO-101 arms](lerobot-so-101.md), whose parts are designed for FDM printing
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [Autodesk tools for CAD](../tech-stack/autodesk.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/formlabs-form-3.md)</sub>
