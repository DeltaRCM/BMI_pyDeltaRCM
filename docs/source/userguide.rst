****************
User Guide
****************


This is the BMI implementation of the pyDeltaRCM model.


.. code::
    
    from BMI_pyDeltaRCM import BmiDelta

    delta = BmiDelta()
    delta.initialize('input_configuration.yml')

    for _ in range(10):
        delta.update()

After you are finished with the model, you can clean up (save any outputs, release memory) with:

.. code::

    delta.finalize()


Input Arguments
---------------

The following CSDMS standard variable names are supported in an input YAML
configuration file.

* 'model_output__out_dir'
* 'model_grid__length'
* 'model_grid__width'
* 'model_grid__cell_size'
* 'land_surface__width'
* 'land_surface__slope'
* 'model__max_iteration'
* 'water__number_parcels'
* 'channel__flow_velocity'
* 'channel__width'
* 'channel__flow_depth'
* 'sea_water_surface__mean_elevation'
* 'sea_water_surface__rate_change_elevation'
* 'sediment__number_parcels'
* 'sediment__bedload_fraction'
* 'sediment__influx_concentration'
* 'model_output__opt_eta_figs'
* 'model_output__opt_stage_figs'
* 'model_output__opt_depth_figs'
* 'model_output__opt_discharge_figs'
* 'model_output__opt_velocity_figs'
* 'model_output__opt_eta_grids'
* 'model_output__opt_stage_grids'
* 'model_output__opt_depth_grids'
* 'model_output__opt_discharge_grids'
* 'model_output__opt_velocity_grids'
* 'model_output__opt_time_interval'
* 'coeff__surface_smoothing'
* 'coeff__under_relaxation__water_surface'
* 'coeff__under_relaxation__water_flow'
* 'coeff__iterations_smoothing_algorithm'
* 'coeff__depth_dependence__water'
* 'coeff__depth_dependence__sand'
* 'coeff__depth_dependence__mud'
* 'coeff__non_linear_exp_sed_flux_flow_velocity'
* 'coeff__sedimentation_lag'
* 'coeff__velocity_deposition_mud'
* 'coeff__velocity_erosion_mud'
* 'coeff__velocity_erosion_sand'
* 'coeff__topographic_diffusion'
* 'basin__opt_subsidence'
* 'basin__maximum_subsidence_rate'
* 'basin__subsidence_start_timestep'
* 'basin__opt_stratigraphy'