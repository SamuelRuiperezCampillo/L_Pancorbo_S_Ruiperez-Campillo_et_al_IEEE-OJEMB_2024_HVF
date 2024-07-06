# L_Pancorbo_S_Ruiperez-Campillo_et_al_IEEE-OJEMB_2024_HVF

This repository contains the functions that compute the analysis of the Vector Field Heterogeneity (VFH) metric from omnipolar electrograms in high-density catheters, corresponding to the publication: L. Pancorbo, S. Ruipérez-Campillo et al., IEEE-OJEMB, 2024.

## Citation
Any individual benefiting from any of this code must cite the work as (APA):


Pancorbo, L., Ruipérez-Campillo, S., Tormos, Á., Guill, A., Cervigón, R., Alberola, A., Chorro, F.J., Millet, J. & Castells, F. (2024). Vector Field Heterogeneity for the Assessment of Locally Disorganised Cardiac Electrical Propagation Wavefronts from High-density Multielectrodes. IEEE Open Journal of Engineering in Medicine and Biology.


### BibTex


@article{pancorbo2023vector,
title={Vector Field Heterogeneity for the Assessment of Locally Disorganised Cardiac Electrical Propagation Wavefronts from High-density Multielectrodes},
author={Pancorbo, Lucía and Ruipérez-Campillo, Samuel and Tormos, Álvaro and Guill, Antonio and Cervigón, Raquel and Alberola, Antonio and Chorro, Francisco Javier and Millet, José and Castells, Francisco},
journal={IEEE Open Journal of Engineering in Medicine and Biology},
year={2024},
volume={5},
pages={32-44},
publisher={IEEE}
}

Please read the description below for usage instructions.

This package has been designed with the following objectives:

Estimate propagation vector maps from unipolar signals
Compute the Vector Field Heterogeneity (VFH) metric.
Compute the Spatial Inhomogeneity (SI) index.
Compute simulations of vector maps with different levels of disorganisation.
The file mainscript.m contains a section for each objective.

Objective 1.

Brief description: Estimate and represent wavefront propagation under the catheter.

STEP 1: To get the bipolar signals execute the following function with specified parameters b_egm=compute_b_egm(u_egm,n_rows,n_columns,mode). This function requires the file rot2D.m.
STEP 2: Estimate propagation angle from the bipolar signals using angle_estimation=compute_angle_estimation(b_egm, n_rows, n_columns)
STEP 3: Rotate the bipolar EGMs accordingly to get the omnipolar signals using the function o_egm = compute_o_egm(b_egm, angle,n_clique_2d)
STEP 4: To visualise the propagation use plot_vector_map(angle_estimation,n_clique_1d)
Function files used: compute_b_egm.m, rot2D.m, compute_angle_estimation.m, compute_o_egm.m, plot_vector_map.m

Objective 2.

Brief description: Compute the Vector Field Heterogeneity (VFH) metric from a propagation map.

STEP 1: To compute the VFH value of a propagation map implement the following function vfh = compute_vfh(angle_estimation,n_clique_1d). This function also requires the function finite_difference.m to work.
STEP 2: To visualise the heterogeneity values of each clique in a map use the function vfh_map=plot_vfh_map(angle_estimation,n_clique_1d)
Function files used: compute_vfh.m, finite_difference.m, plot_vfh_map.m

Objective 3.

Brief description: Compute the Spatial Inhomogeneity (SI) index from the activation map.

STEP 1: Compute the Local Activation Times (LATs) from the unipolar signals using the function compute_lats(u_egm,sampling_freq,n_grid_2d)
STEP 2: To visualise the relative LATs map in which the first activated electrode is the zero, use lat_map=plot_lat_relative_map(lat,n_grid_1d)
STEP 3: The function si=compute_si(lat_map,n_grid_1d) computes the SI index. The algorithm is based on the work W. J. Lammers, et al. "Quantification of spatial inhomogeneity in conduction and initiation of reentrant atrial arrhythmias." American Journal of Physiology-Heart and Circulatory Physiology (1990).
STEP 4: Plot the map of phase differences according to the methodology proposed by Lammers et al. (1990) with the function phase_map=plot_phase_map(lat_map,n_grid_1d)
STEP 5: To visualise the phase differences in a histogram run the function plot_phase_histogram(lat_map,n_grid_1d)
Function files used: compute_lats.m, plot_lat_relative_map.m, compute_si.m, plot_phase_map.m, plot_phase_histogram.m

Objective 4.

Brief description: Simulate propagation vector maps with increasing levels of heterogeneity or disorganisation to test the VFH metric.

STEP 1: Simulate a vector map with random angles from a specified interval using the function simulated_angle=simulate_vector_map(angle_interval,n_clique_1d). plot_vector_map.m can be used to visualise the propagation.
STEP 2: The function vfh_results=vfh_simulated_data(n_clique_1d,N) generates N vector maps for angular intervals starting at ±1º and from ±5º to ±180º in steps of 5º, and computes the VFH metric for each of them. Note that this function requires the files simulate_vector_map.m and compute_vfh.m.
Function files used: simulate_vector_map.m, vfh_simulated_data.m, compute_vfh.m.
