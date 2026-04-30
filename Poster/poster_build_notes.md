# Moss Poster Requirements and Build Notes

## Goal

Create a polished scientific poster based on the PowerPoint template:

- `Poster/42x60 Poster Template - FINAL_2023 (1).pptx`

The poster should summarize the article:

- `Poster/moss_technical_note_scientific_revision.pdf`

Final deliverables should be both:

- `Poster/moss_spontaneous_colonization_poster.pptx`
- `Poster/moss_spontaneous_colonization_poster.pdf`

## User Requirements

- The poster must be in English.
- Quality is important; the poster should be as polished as possible, not only a quick draft.
- The template may be rearranged if needed to make the scientific story clearer.
- The poster should incorporate Joel Maldonado's content notes from:
  - `Poster/Findings-content.md.md`
- Technical and administrative details should be taken from the previous poster:
  - `Poster/previous-version.pdf`
- The author line should be:
  - Freddy Aguilar, Sophia Bui, Ava Mohr
  - The University of Arizona, Department of Mathematics
- Logos should be taken from the previous poster:
  - University of Arizona / College of Science / Mathematics
  - Biosphere 2
- The center of the poster should contain the preliminary images from:
  - `img/LEO_2022_11_22_cropped_rectified_rectangle.png`
  - `img/persistent_moss_map.png`
  - `img/moss_cross_sections.png`
- These center images are placeholders for now. Their exact content may change later, but the number and approximate size of image slots should remain the same.

## Scientific Story Used

The poster follows the three-act structure described in Joel Maldonado's notes:

1. Why this system matters:
   - Spontaneous moss colonization occurred on a crushed-basalt, Mars-analog substrate in Biosphere 2's LEO Observatory.
   - The key question is whether the colonization pattern is random or structured by hillslope geometry.

2. How the system was measured:
   - The imaging pipeline requires calibration, stitching, and a broad moss proxy.
   - A single-date color threshold is unreliable because moss color changes with hydration and irrigation state.
   - The robust response variable is multi-date persistence, not raw greenness.

3. What the topography shows:
   - Moss persistence is concentrated on off-center shoulder zones.
   - The deepest and wettest drainage corridor is not the most favorable habitat.
   - The pattern supports a bounded moisture optimum rather than a monotone "wetter is better" interpretation.

## Poster Structure

The final poster uses one landscape slide with the same aspect ratio as the template:

- PowerPoint size: `30 x 21 in`
- Equivalent print ratio: `60 x 42 in`

The layout is organized into three columns:

- Left column:
  - motivation and system description
  - research questions
  - experimental setup
  - previous work
  - data and time window
  - poster story

- Center column:
  - image-to-moss methodology pipeline
  - three central image panels from `img/`
  - Findings 01-02: spatial persistence and color-thresholding caveat
  - summary statistics

- Right column:
  - Finding 03: topographic control
  - response curves and model calibration from the technical note
  - logistic suitability ranking model
  - candidate mechanisms for trough suppression
  - conclusions and next steps

## Key Technical Content Included

Statistics and model details were taken from the technical note and Joel's notes:

- 26.6% of cells stable on at least two dates
- 7.1% of cells strong on all three dates
- median lateral offset of stable moss zone: 3.7 m
- median trough depth of stable moss zone: 0.088 m
- logistic suitability ranking model:
  - `logit P(M=1) = beta0 + beta_w W - beta_f F - gamma(d-d0)^2 + beta_t T`
- model performance:
  - training AUC: 0.724
  - spatial cross-validated AUC: 0.657
- depth optimum:
  - `d0 = 0.407 m`

## Assets Created or Extracted

The following reusable poster assets were created in `Poster/`:

- `ua_math_logo.png`
  - extracted from `previous-version.pdf`
  - University of Arizona / College of Science / Mathematics logo

- `biosphere2_logo.png`
  - extracted from `previous-version.pdf`
  - Biosphere 2 logo

- `moss_response_curves.png`
  - extracted from `moss_technical_note_scientific_revision.pdf`
  - used in the quantitative evidence section

- `stable_moss_calibration.png`
  - extracted from `moss_technical_note_scientific_revision.pdf`
  - used in the quantitative evidence section

## Build Method

The poster was generated with:

- `Poster/build_moss_poster.py`

The script:

1. Opens the original PowerPoint template.
2. Keeps one slide and preserves the `30 x 21 in` slide size.
3. Clears the placeholder content.
4. Adds the header, logos, author block, and three-column scientific layout.
5. Inserts the three central preliminary images from `img/`.
6. Inserts supporting quantitative figures extracted from the technical note.
7. Saves the PowerPoint file.
8. Generates a matching PDF using ReportLab.

The PDF was generated directly from the same scripted layout rather than exported through LibreOffice, because this environment had LibreOffice Writer/Calc installed but did not have LibreOffice Impress available for reliable PPTX-to-PDF conversion.

## Rebuild Command

The poster can be regenerated with:

```bash
/tmp/moss_poster_venv/bin/python Poster/build_moss_poster.py
```

During the original build, the temporary virtual environment contained:

- `python-pptx`
- `reportlab`
- `Pillow`

If rebuilding on a new machine, create a Python environment and install those packages first.

## Verification Performed

The generated files were checked as follows:

- The PPTX archive passed `unzip -t`.
- The PPTX contains one slide.
- The PPTX slide size is `30 x 21 in`.
- The PDF contains one page.
- The PDF page size is `2160 x 1512 pt`, matching the `30 x 21 in` poster.
- A raster preview of the PDF was generated with `pdftoppm` and visually inspected for layout, image placement, logo rendering, and obvious text overlap.

