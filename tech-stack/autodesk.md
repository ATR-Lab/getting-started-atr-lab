# Autodesk Fusion and Inventor

> **Read this when** you need to design a part, mount or gripper, get a free education license, send a model to the Form 3 printer, or turn a CAD model into meshes and a URDF for simulation.

Autodesk Fusion and Autodesk Inventor are 3D CAD (computer-aided design) programs: you draw parts with exact dimensions, put them together in assemblies and export them for printing, machining or simulation. Students and educators at Kent State can get both free through the Autodesk Education program. The one thing to remember: keep the native CAD file (`.f3d`, `.ipt`, `.iam`) as the source and treat every STL, 3MF or mesh as an export you can regenerate.

## Contents

- [Which one to use](#which-one-to-use)
- [Get an education license](#get-an-education-license)
- [From CAD to the Form 3 printer](#from-cad-to-the-form-3-printer)
- [From CAD to simulation](#from-cad-to-simulation)
- [File naming and storage](#file-naming-and-storage)
- [Related](#related)

## Which one to use

| | Fusion | Inventor |
| --- | --- | --- |
| Runs on | Windows, macOS and Chromebook ([Autodesk](https://www.autodesk.com/education/edu-software/fusion)) | Windows only; Inventor 2027 needs 64-bit Windows 11 ([system requirements](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/System-requirements-for-Autodesk-Inventor-2027.html)) |
| Files | Stored in Autodesk's cloud; export `.f3d` or `.f3z` archives to keep a copy | Local `.ipt` parts and `.iam` assemblies |
| Good for in the lab | Brackets, sensor mounts, enclosures and grippers to 3D print; quick assemblies; sharing a design with a teammate | Large mechanical assemblies and detailed engineering drawings |

The lab's default for new designs: [Fusion or Inventor: lab decision]. Either can export the formats below.

## Get an education license

Autodesk Education gives eligible students and educators "free, one-year, single-user access to Autodesk software for educational purposes", renewable each year while you remain eligible ([Autodesk Education](https://www.autodesk.com/education/edu-software/overview)).

1. Create an Autodesk account with your Kent State email.
2. Confirm your eligibility: you must meet the minimum age and be enrolled at, or work for, a qualified educational institution ([eligibility](https://www.autodesk.com/support/account/education/students-educators/eligibility)). Autodesk checks this through SheerID; students may need to upload an enrollment document ([how to verify](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/How-to-verify-your-student-eligibility.html)).
3. Download Fusion or Inventor from the education page and sign in.

> [!IMPORTANT]
> Education licenses are for "learning, teaching, or educational research", not for commercial, professional or for-profit work ([Autodesk: educational purposes](https://www.autodesk.com/company/educational-purposes)). Before you use an education license on a project funded by or delivered to a company, ask [lab manager name] whether the project needs a commercial license.

## From CAD to the Form 3 printer

The lab's resin printer is prepared in Formlabs PreForm (version 3.63.1, Sept. 25, 2026, for Windows 10 64-bit or later and macOS 13 or later; [release notes](https://formlabs.com/support/PreForm-Release-Notes)).

1. In Fusion, export the body as a mesh: **File > Export** or **Save As Mesh**, as STL or 3MF ([Autodesk](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/How-to-export-an-STL-file-from-Fusion-360.html)). In Inventor, use **File > Save As > Save Copy As** and choose STL, and check the units under **Options** ([Autodesk](https://help.autodesk.com/cloudhelp/2015/ENU/Inventor-Help/files/GUID-59FB702C-F37A-4DEA-ADCF-51AD8A219C9B.htm)).
2. Open the file in [PreForm](https://formlabs.com/software/preform/). PreForm opens STL, OBJ and 3MF meshes and also CAD files directly, including STEP and Inventor `.ipt` and `.iam` ([Formlabs](https://formlabs.com/support/Opening-a-model-in-PreForm)).
3. Check the units and scale after import; a part that arrives 25.4 times too big or small was exported in inches instead of millimeters.
4. Printing, washing and curing rules, including resin safety, are on the [Formlabs Form 3 page](../hardware/formlabs-form-3.md) and in the [safety rules](../lab-rules/safety.md#3d-printing-and-resin).

## From CAD to simulation

Simulators need two things from your CAD model: meshes for what the robot looks like and collides with, and a description of links, joints and masses. In ROS 2 that description is a URDF (Unified Robot Description Format) file.

- **Meshes:** export each rigid link as its own STL, OBJ or (for Gazebo and Isaac Sim) DAE or USD file, in meters, with the origin where the joint will be. Simplify collision meshes; a convex hull or a few boxes simulate faster and more stably than the visual mesh.
- **URDF exporters for Fusion:** these are open-source add-ins written by the community, not Autodesk or ROS products. The ROS 2 documentation keeps a list of CAD exporters and says the core maintainers "do not maintain these packages" ([Generating an URDF file](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/URDF/Exporting-an-URDF-File.html)). Fusion add-ins that were updated recently (checked on GitHub, Sept. 30, 2026):

  | Add-in | Exports | Last commit |
  | --- | --- | --- |
  | [fusion2URDF](https://github.com/Adriaeik/fusion2URDF) (MIT; on the ROS 2 docs list) | URDF with ros2_control tags and closed loops | Sept. 2026 |
  | [ACDC4Robot](https://github.com/ACDC4Robot/Fusion360) (MIT) | URDF, SDF (Gazebo) and MJCF (MuJoCo) | Aug. 2026 |

  Older add-ins, such as the original `fusion2urdf`, have not been updated for a year or more. Check the README of whichever you choose for the Fusion and ROS 2 versions it supports.

- **Check the result** before you trust it: open the URDF in RViz (`ros2 launch urdf_tutorial display.launch.py model:=/path/to/robot.urdf` after `sudo apt install ros-jazzy-urdf-tutorial`), move every joint, and compare masses and joint limits with the real robot.
- Then import it into [Gazebo](gazebo.md), [Isaac Sim](isaac-sim.md) (URDF importer) or [MuJoCo](mujoco.md) (MuJoCo can compile URDF, or use the MJCF export).

## File naming and storage

Follow the CAD and hardware file conventions in the dev guidelines' [hardware page](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/hardware.md): names, revisions, exports and bills of materials. In short:

- Keep the native file as the source of truth and store exports (STL, 3MF, STEP, meshes) next to it, named so anyone can tell which revision they came from.
- Save CAD files in [CAD file location], not only in a personal Autodesk cloud account, which you lose when you leave Kent State.
- Put URDF and meshes that a robot's software needs in that robot's Git repository.

## Related

- [Tech stack](README.md)
- [Formlabs Form 3](../hardware/formlabs-form-3.md)
- [Gazebo](gazebo.md), [Isaac Sim](isaac-sim.md) and [MuJoCo](mujoco.md)
- [Unity](unity.md): CAD models in XR scenes
- [Dev guidelines: hardware](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/hardware.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/autodesk.md)</sub>
