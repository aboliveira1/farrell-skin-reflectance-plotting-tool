# Diffuse Reflectance Spectrum of Skin Using Farrell's Model

This Jupyter Notebook provides a set of functions for plotting the reflectance spectra of skin based on the Farrell diffusion theory. The notebook includes functions to load spectral data, calculate optical properties, and visualize reflectance spectra by varying different parameters.

## How to Use This Notebook

### Loading Spectral Data

First, load the spectral data from a `.mat` file:

```python
nmLIB, MU = load_spectral_data(filename='AbsorptionScatteringCoefficients.mat')
```

### Plotting a Single Spectrum

You can plot a single reflectance spectrum using default parameters:

```python
default_params = {
    'blood_content': 0.02,  # 2% Blood content
    'oxygen_saturation': 0.95,  # 95% Oxygen saturation
    'water_content': 0.70,  # 70% Water content
    'refractive_index_ratio': 1.4,  # Refractive index ratio
    'melanin_content': 0.05,  # 5% Melanin content
    'collagen_content': 0.0  # 0% Collagen content
}

plot_single_spectrum(default_params, nmLIB, MU, show_params=True, use_gradient=False)
```

If you want a gradient background for the plot:

```python
plot_single_spectrum(default_params, nmLIB, MU, show_params=True, use_gradient=True)
```

### Varying a Single Parameter

To visualize how the reflectance spectrum changes with varying a single parameter:

```python
plot_varying_parameter('oxygen_saturation', 0.7, 1.0, 12, nmLIB, MU, default_params, use_gradient=False)
```

If you prefer a gradient background:

```python
plot_varying_parameter('oxygen_saturation', 0.7, 1.0, 12, nmLIB, MU, default_params, use_gradient=True)
```

### Varying Multiple Parameters

You can also vary multiple parameters simultaneously:

```python
param_ranges = {
    'blood_content': (0.01, 0.1, 12),  # 1% to 10%
    'oxygen_saturation': (0.7, 1.0, 12),  # 70% to 100%
    # Add other parameters if needed
}

plot_varying_multiple_parameters(param_ranges, nmLIB, MU, default_params, use_gradient=False)
```

For a plot with a gradient background:

```python
plot_varying_multiple_parameters(param_ranges, nmLIB, MU, default_params, use_gradient=True)
```

### Functions Overview

- **`get_rd_farrell(mua, musp, n)`**: Calculates the diffuse reflectance using Farrell's model.
- **`load_spectral_data(filename)`**: Loads spectral data from a `.mat` file.
- **`filter_wavelengths(nmLIB, mua, musp, min_wl, max_wl)`**: Filters the wavelengths within a specified range.
- **`draw_gradient_background(fig, color1, color2)`**: Draws a gradient background for the plot.
- **`plot_spectra(nmLIB, reflectances, labels, title, xlabel, ylabel, use_gradient)`**: Plots reflectance spectra.
- **`save_data(nmLIB, reflectances, labels, params, filename)`**: Saves the reflectance data and parameters to a file.
- **`calculate_mua(MU, params, nmLIB)`**: Calculates the absorption coefficient based on given parameters.
- **`default_musp(nmLIB)`**: Calculates the reduced scattering coefficient based on a power law model.
- **`plot_single_spectrum(params, nmLIB, MU, save, save_filename, only_save, show_params, use_gradient)`**: Plots a single reflectance spectrum.
- **`plot_varying_parameter(param_name, min_value, max_value, num_steps, nmLIB, MU, default_params, save, save_filename, only_save, use_gradient)`**: Plots reflectance spectra by varying a single parameter.
- **`plot_varying_multiple_parameters(param_ranges, nmLIB, MU, default_params, save, save_filename, only_save, use_gradient)`**: Plots reflectance spectra by varying multiple parameters.

This notebook is designed to help users understand the impact of various physiological parameters on the diffuse reflectance of skin, using Farrell's diffusion theory. It provides an easy-to-use interface for loading data, performing calculations, and visualizing the results.

### Citation

The implementation is based on the following paper:
Farrell, T. J., Patterson, M. S., & Wilson, B. (1992). A diffusion theory model of spatially resolved, steady-state diffuse reflectance for the noninvasive determination of tissue optical properties in vivo. Medical Physics, 19(4), 879-888.
