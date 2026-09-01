# Cortical Phosphene Vision Simulator

An interactive, real-time simulation of camera-based visual encoding for a hypothetical penetrating-electrode array in human primary visual cortex (V1).

**[Launch the simulator](https://patrickjendritza.com/phosphene-vision-simulator/)**

The application runs entirely in the browser. Webcam frames are processed locally and are not uploaded to a server.

## Demo

https://github.com/user-attachments/assets/1c9613af-9846-43a3-a04d-b11c63b660fb

## Overview

Cortical visual prostheses aim to create visual percepts by stimulating the visual cortex directly. Electrical stimulation of V1 can evoke localized spots of light called *phosphenes*. A future prosthesis could use a camera to transform a visual scene into patterns of stimulation across many cortical electrodes.

This simulator provides an accessible visualization of that general idea. Each simulated electrode samples a camera-derived activation map and produces a localized Gaussian phosphene. Electrode placement can follow a simplified model of human V1 cortical magnification, producing a higher density of stimulation sites near central vision. Phosphene size increases with eccentricity because the same estimated cortical activation spread covers a larger region of visual space in peripheral representations.

The simulator is intended for research visualization, teaching, and public engagement. It is not a prediction of what any individual implant recipient would perceive.

## Features

- Live webcam input with real-time browser-based processing
- Configurable array size from 1 to 10,000 stimulation sites
- Human V1 cortical-magnification model or uniform visual-field spacing
- Adjustable field of view and eccentricity-dependent phosphene size
- Fixed electrode dropout, positional irregularity, gain variability, and threshold variability
- Three visual encoding strategies:
  - **Sobel boundaries:** emphasizes local luminance gradients and object boundaries
  - **Luminance:** directly encodes grayscale image intensity
  - **Luminance + Sobel:** combines surface brightness with boundary information
- Optional phenomenological phosphene adaptation and recovery
- Diagnostic views showing the camera image, grayscale image, Sobel map, encoded image, and sampled electrode activity
- No installation, backend, or data upload required

## How the simulation works

1. The webcam image is resized and converted to grayscale.
2. The selected encoder generates a luminance, Sobel-boundary, or hybrid activation map.
3. Simulated electrodes sample this map at their visual-field locations.
4. Electrode-specific thresholds, gain differences, dropout, and positional irregularity are applied.
5. Active electrodes generate Gaussian phosphene profiles whose size depends on estimated cortical current spread and local cortical magnification.
6. The phosphene profiles are summed to generate the simulated percept.

For the cortical-spacing condition, local magnification is approximated as

$$
M(E)=\frac{17.3}{E+0.75}\quad \text{mm/degree},
$$

where $E$ is visual eccentricity in degrees. Phosphene extent is estimated from a penetrating-electrode current-spread reference and converted from cortical distance into visual angle using the local magnification factor.

## Parameters

| Parameter | Meaning |
| --- | --- |
| Field of view | Diameter of the camera-centred visual field represented by the array |
| Electrodes | Number of available stimulation sites before dropout |
| Processing model | Visual information used to drive the electrodes |
| Electrode spacing | V1-inspired cortical magnification or uniform visual-angle density |
| Phosphene size | Scale factor applied to the current-spread-derived phosphene estimate |
| Electrode dropout | Proportion of sites that never generate a phosphene |
| Position irregularity | Fixed displacement relative to local electrode spacing |
| Activation threshold | Minimum encoder intensity needed to activate an electrode |
| Boundary contribution | Sobel weight in the hybrid encoding mode |
| Adaptation | Optional attenuation during sustained activation and recovery while inactive |

## Limitations

The model deliberately simplifies cortical prosthetic vision. In particular, it assumes circular Gaussian phosphenes and linear summation across electrodes. It does not model:

- Patient-specific retinotopy or electrode placement
- The folded three-dimensional geometry of V1
- Eye movements or gaze-contingent camera stabilization
- Nonlinear interactions between simultaneously stimulated electrodes
- Detailed electrical pulse trains or stimulation-safety constraints
- The full variability of phosphene shape, color, and temporal dynamics reported by human participants

The 10,000-electrode setting is an exploratory visualization, not a claim about the feasibility or effective resolution of a current clinical device. Electrode count also does not necessarily equal the number of distinct, stable, and usable phosphenes.

## Running locally

The hosted version is the easiest way to use the simulator:

**https://patrickjendritza.com/phosphene-vision-simulator/**

Alternatively, clone or download the repository and serve it from a local web server:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` and grant camera permission. Directly opening `index.html` as a local file may prevent webcam access in some browsers.

## Scientific references

1. van der Grinten M, et al. (2024). [Towards biologically plausible phosphene simulation for the differentiable optimization of visual cortical prostheses](https://doi.org/10.7554/eLife.85812). *eLife*, 13, e85812.
2. Horton JC, Hoyt WF. (1991). [The representation of the visual field in human striate cortex](https://doi.org/10.1001/archopht.1991.01080060080030). *Archives of Ophthalmology*, 109, 816–824.
3. Bosking WH, et al. (2017). [Saturation in phosphene size with increasing current levels delivered to human visual cortex](https://doi.org/10.1523/JNEUROSCI.2896-16.2017). *Journal of Neuroscience*, 37, 7188–7197.
4. Tehovnik EJ, Slocum WM. (2007). [Phosphene induction by microstimulation of macaque V1](https://pubmed.ncbi.nlm.nih.gov/17173976/). *Brain Research Reviews*, 53, 337–343.
5. Schmidt EM, et al. (1996). [Feasibility of a visual prosthesis for the blind based on intracortical microstimulation of the visual cortex](https://doi.org/10.1093/brain/119.2.507). *Brain*, 119, 507–522.
6. Fernández E, et al. (2021). [Visual percepts evoked with an intracortical 96-channel microelectrode array inserted in human occipital cortex](https://www.jci.org/articles/view/151331). *Journal of Clinical Investigation*, 131, e151331.
7. Beauchamp MS, et al. (2020). [Dynamic stimulation of visual cortex produces form vision in sighted and blind humans](https://doi.org/10.1016/j.cell.2020.04.033). *Cell*, 181, 774–783.e5.

## Author

Created by **Patrick Jendritza**, 2026.

## Citation

If you use the simulator in teaching, demonstrations, or research, please cite the project:

```bibtex
@software{jendritza2026phosphene,
  author = {Jendritza, Patrick},
  title = {Cortical Phosphene Vision Simulator},
  year = {2026},
  url = {https://patrickjendritza.com/phosphene-vision-simulator/}
}
```



