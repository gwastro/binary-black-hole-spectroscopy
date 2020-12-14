# Binary black hole spectroscopy: a no-hair test of GW190814 and GW190412
**Collin D. Capano<sup>1,2</sup>, Alexander H. Nitz<sup>1,2</sup>**

 <sub>1. [Albert-Einstein-Institut, Max-Planck-Institut for Gravitationsphysik, D-30167 Hannover, Germany](http://www.aei.mpg.de/obs-rel-cos)</sub>  

 <sub>2. Leibniz Universitat Hannover, D-30167 Hannover, Germany</sub> 

This repository is a companion to [Capano and Nitz (arXiv:2008.02248)](https://arxiv.org/abs/2008.02248). It contains posterior probability density files from the parameter estimation analysis described in the paper and the configuration files needed to run the analysis. We also provide a jupyter a notebook for combining results between GW190814 and GW190412. We encourage use of these data in derivative works. If you use the material provided here, please cite the paper using the reference:
```
@article{Capano:2020dix,
    author = "Capano, Collin D. and Nitz, Alexander H.",
    title = "{Binary black hole spectroscopy: a no-hair test of GW190814 and GW190412}",
    eprint = "2008.02248",
    archivePrefix = "arXiv",
    primaryClass = "gr-qc",
    month = "8",
    year = "2020"
}
```

## l = 2, m = 1 results ##

In the paper we only showed results for the $\ell m = 33$ mode. The following violin plots are equivalent to Fig. 2 of the paper, but for the $\ell m = 21$ mode:

![GW190412](violinplot-gw190412-21.png)

![GW190814](violinplot-gw190814-21.png)

Green regions/lines are from the analysis in which we allow both the masses and spins to deviate. Dark blue lines show the same result when the sub-dominant mode spins are fixed to the dominant-mode value. Horizontal hashes indicate the median (center) and 90\% credible regions. Gray lines show the marginalized prior distributions. Since the prior distributions on the $\Delta \chi_{ik, \ell m}$ are dependent on the dominant-mode spins $\chi_{ik, 22}$, we show spin priors conditioned on the $\chi_{ik, 22}$ posteriors.

We see that we obtain negligible constraints from the 21 mode. This is expected, as the 33 mode was the only sub-dominant harmonic with appreciable SNR in both events.

## Software

The analysis may be replicated using [PyCBC](pycbc.org) version 1.16.5 or later. In order to run the analysis, the [modified_hm_waveforms](https://github.com/cdcapano/modified_hm_waveforms) plugin must be installed. This package is what allows parameters to be modified separately for each sub-dominant harmonic. To install, first install `pycbc` using pip, then clone and install the `modified_hm_waveforms` plugin:
```
pip install "pycbc>=1.16.5"
git clone https://github.com/cdcapano/modified_hm_waveforms
cd modified_hm_waveforms
python setup.py install
```

Once the `modified_hm_waveforms` package is installed, `pycbc` will automatically detect it at runtime; you do not need to reinstall pycbc in order to use it.

## Posterior files ##

HDF files containing posterior samples for GW190412 and GW190814 may be found in the `posteriors` directory. The `posterior-all_params.hdf` file for each event contains the posterior samples from the analysis in which we allow the masses, phase, *and* spins measured by the sub-dominant harmonics to deviate from the dominant harmonic. The `posterior-mass_params.hdf` contains samples from the analysis in which we only allow phase and mass parameters to deviate.

Samples are stored as 1D arrays in the `samples` group in the posterior files. There is a separate dataset for each parameter that was varied in the analysis, along with a dataset for the log likelihood at that point. The parameters are:

Parameter | Description
--------- | -----------
`srcmass1` | The source-frame mass of the larger object, in solar masses.
`srcmass2` | The source-frame mass of the smaller object, in solar masses.
`spin1_a` | The magnitude of the dimensionless spin of the larger object.
`spin2_a` | "" smaller object.
`spin1_azimuthal` | The azimuthal angle of the dimensionless spin of the larger object.
`spin2_azimuthal` | "" smaller object.
`spin1_polar`| The polar angle of the dimensionless spin of the smaller object.
`spin2_polar` | "" smaller object.
`coa_phase` | The reference phase.
`ra` | The right ascension of the binary, in radians.
`dec` | The declination of the binary, in radians.
`comoving_volume` | The comoving volume (in Mpc<sup>3</sup>). To convert to luminosity distance we use standard Lambda-CDM cosmology, with values from the [Planck 2015 results](https://doi.org/10.1051/0004-6361/201525830).
`inclination` | The angle between the orbital angular momentum and the line of sight to the binary at the reference frequency (stored as `f_ref` in the file's `attrs`), in radians.
`polarization` | The polarization angle of the gravitational wave, in radians.
`delta_tc` | The difference between the measured coalescence time of the event and a reference GPS time, which is stored in the file's `attrs` as `trigger_time`.
`fdiff_33_mchirp` | The fractional difference in the chirp mass between the 33 mode and the dominant mode.
`fdiff_21_mchirp` | "" 21 mode "".
`fdiff_33_eta` | The fractional difference in the symmetric mass ratio between the 33 mode and the dominant mode.
`fdiff_21_eta` | "" 21 mode "".
`absdiff_33_coa_phase` | The difference in the reference phase between the 33 mode and the dominant mode.
`absdiff_21_coa_phase` | "" 21 mode ""
`spin1_33_a` | (*not in the `mass_params` files*) The magnitude of the dimensionless spin of the larger object, as measured by the 33 mode.
`spin1_21_a` | "" 21 mode.
`spin1_33_azimuthal` | (*not in the `mass_params` files*) The azimuthal angle of the dimensionless spin of the smaller object, as measured by the 33 mode.
`spin1_21_azimuthal` | "" 21 mode.
`spin1_33_polar` | (*not in the `mass_params` files*) The polar angle of the dimensionless spin of the smaller object, as measured by the 33 mode.
`spin1_21_polar` | "" 21 mode.
`spin2_33_a` | (*not in the `mass_params` files*) The magnitude of the dimensionless spin of the smaller object, as measured by the 33 mode.
`spin2_21_a` | "" 21 mode. 
`spin2_33_azimuthal` | (*not in the `mass_params` files*) The azimuthal angle of the dimensionless spin of the smaller object, as measured by the 33 mode.
`spin2_21_azimuthal` | "" 21 mode.
`spin2_33_polar` | (*not in the `mass_params` files*) The polar angle of the dimensionless spin of the smaller object, as measured by the 33 mode.
`spin2_21_polar` | "" 21 mode.
`loglikelihood` | The log of the likelihood at the given point.

The files contain metadata about the analysis, including the parameters that were fixed. These can be found in the files' `attrs`.

The data that was analyzed is also stored in the files, in the `data/{ifo}` where `{ifo}` is the detector (H1, L1, or V1). The `data/{ifo}/stilde` is a 1D array of the data in the frequency domain. The size of the frequency steps and the GPS start time of the data is stored in the `attrs` of the dataset. A highpass filter has been applied to the data to remove large low-frequency noise.

The PSDs that were used in the analyses may also be found in the `data` group, in `data/{ifo}/psds/0`. This is also a (real) frequency series; the size of the frequency steps are stored in the `attrs` of the dataset. You can plot the PSDs in the files using `pycbc_plot_psd_file`; example usage:
```
pycbc_plot_psd_file --psd-files {posterior_file} --hdf-group data --dyn-range-factor 1 --output-file psds.png
```

## Configuration files

The configuration files used in the analyses are in the `configuration` directory. These specify the prior, sampler, model used, and the data analyzed. The analyses may be replicated using by passing these files to the `pycbc_inference` executable. See the [pycbc inference documentation](http://pycbc.org/pycbc/latest/html/inference.html) for more details on usage.

## Combining results

The notebook [CombineResults.ipynb](CombineResults.ipynb) is what we used to combine the posteriors on chirp mass and symmetric mass ratio deviations between GW190412 and GW190814. The notebook can be run on the posterior files in this repository.

## License ##
![Creative Commons License](https://i.creativecommons.org/l/by-sa/3.0/us/88x31.png "Creative Commons License")

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 United States License](http://creativecommons.org/licenses/by-sa/3.0/us/).
