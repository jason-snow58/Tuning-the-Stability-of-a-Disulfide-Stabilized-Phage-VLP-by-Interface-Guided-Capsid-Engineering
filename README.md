# Tuning-the-Stability-of-a-Disulfide-Stabilized-Phage-VLP-by-Interface-Guided-Capsid-Engineering
Google Colab notebooks supporting the analysis in "Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering"

Built for Google Colab. Each notebook reproduces one analysis from the paper,
end to end, from a coordinate file you supply. Nothing needs to be installed
first and nothing needs to be configured.

| notebook | paper figure | needs PyMOL |
|---|---|---|
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure 1_interface_classification.ipynb` | **Figure 1** — interdimer/intradimer/bridge classification | no |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure2 C_contact_maps.ipynb` | **Figure 2C** — contact detection | **yes** |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Interdimer_interface_residue_contact_detection.ipynb` | **Figure 2C** — map panels | no |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_c-alpha_interface_map.ipynb` | presentation tool, no figure | **yes** |

The filenames still carry the numbering the figures had in an earlier draft.
The paper figure column is the current one: the contact classification is now
Figure 1, and the contact maps are panel C of Figure 2.

Two notebooks feed two others. `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure 1_interface_classification.ipynb` writes the
`.pml` that `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_c-alpha_interface_map.ipynb` opens, and `figure3c_contact_detection`
writes the contact table that `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure2 C_contact_maps.ipynb` draws.

## Running one

1. In Colab, **File → Upload notebook**, or **File → Open notebook → GitHub**
   and paste the repository URL.
2. **Runtime → Run all.** A standard CPU runtime is enough; none of this uses
   a GPU.
3. The first cell is a form. It detects Colab, installs what is missing,
   and shows the input settings. The defaults are the published values, so
   running it unchanged reproduces the published tables.
4. When a notebook needs a file it does not have, it shows an upload box.
   Pick your coordinate file and it continues.
5. Finished files download to your machine on their own. They are also in the
   session under the folder icon in the left sidebar if you want to look at
   them before they leave.

Installing PyMOL takes about a minute in the two notebooks that need it, and
happens once per session.

## What you need to supply

| notebook | input |
|---|---|
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure 1_interface_classification.ipynb` | a q3-axis coordinate file (`.pdb`) |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Interdimer_interface_residue_contact_detection.ipynb` | any structure (`.pdb`) |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_Figure2 C_contact_maps.ipynb` | the contact table written by the detection notebook |
| `Tuning the Stability of a Disulfide-Stabilized Phage VLP by Interface-Guided Capsid Engineering_c-alpha_interface_map.ipynb` | the `.pml` written by the classification notebook |

**Segment identifiers must survive into the file you upload.** In these
assemblies the chain column is degenerate — several subunits share one chain
letter — so the analysis keys on the segment identifier instead. A file saved
in a way that drops segments will merge subunits that are not the same subunit.

A Colab session is wiped when it disconnects. Re-upload your input, or mount
Drive from the sidebar if you would rather keep it between sessions.

## Running somewhere other than Colab

The notebooks work in any Jupyter kernel. Outside Colab nothing is installed
for you, so the kernel needs `numpy`, `mdanalysis`, `matplotlib`, and
`pymol-open-source` for the two PyMOL notebooks. Inputs are then read from the
folder the notebook is running in, and outputs are written beside them instead
of being downloaded.

## How the notebooks are built

One analysis per notebook, and each notebook carries the analysis package with
it — there is nothing to clone and no repository to be online for. Cells near
the top write the package into the session, then the analysis cells import it.

The Figure 1 notebook keeps its four phases in four separate cells, each
stating what it may and may not do: **decide** is the only cell that reads a
structure or classifies anything, **render** turns the resulting record into
finished bytes without reading or writing, **validate** derives the same rows
three independent ways and compares them, and **effect** does nothing but put
bytes on disk. The other three notebooks wrap producers that read, decide,
draw and write in one operation, and say so rather than pretending to a
separation they do not have.

These files are generated. Editing a notebook edits a copy — change the package
and rebuild, so that what runs here cannot drift from the code that was
verified.
