****************
User Guide
****************


This is the BMI implementation of the pyDeltaRCM model.



Examples
--------

Basic run
~~~~~~~~~



.. plot::
    :context: reset
    :include-source:

    from BMI_pyDeltaRCM import BmiDelta

    delta = BmiDelta()
    delta.initialize()

    for _ in range(3):
        delta.update()

Three timesteps produces only a small mouth bar deposit.

.. plot::
    :context:
    :include-source:

    import matplotlib.pyplot as plt

    fig, ax = plt.subplots()
    im = ax.imshow(delta.get_value('sea_bottom_surface__elevation'))
    plt.colorbar(im, ax=ax, shrink=0.5)
    plt.show()

After you are finished with the model, you can clean up (save any outputs, release memory) with:

.. plot::
    :context: close-figs
    :include-source:

    delta.finalize()

.. hint::

    Pass a path to a YAML file to :obj:`initialize` to use a configuration file to set up the BmiDelta model.

    :code:`mdl.initialize(filename='input_configuration.yml'`)


Changing runtime values
~~~~~~~~~~~~~~~~~~~~~~~

Change the bedload fraction input on each timestep.

.. plot::
    :context: close-figs
    :include-source:

    delta = BmiDelta()
    delta.initialize()

    for i in range(3):
        delta.set_value('channel_exit_water_sediment~bedload__volume_fraction', (i/2))
        delta.update()
    
    fig, ax = plt.subplots()
    im = ax.imshow(delta.get_value('sea_bottom_surface__elevation'))
    ax.set_title('end f_bedload: {0}'.format(delta._delta.f_bedload))
    plt.colorbar(im, ax=ax, shrink=0.5)    
    plt.show()


.. plot::
    :context: close-figs
    :include-source:

    delta.finalize()


Input Parameters
----------------

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


Runtime Parameters
------------------

The following CSDMS standard variable names are supported to be viewed and changed during model runtime (using :obj:`get_value` and :obj:`set_value`). 
Key in brackets indicates the underlying pyDeltaRCM `DeltaModel` attribute that is viewed/changed via the BMI.

* 'channel_exit_water_flow__speed' ['u0']
* 'channel_exit_water_x-section__width' ['N0_meters']
* 'channel_exit_water_x-section__depth' ['h0']
* 'sea_water_surface__mean_elevation' ['H_SL']
* 'sea_water_surface__rate_change_elevation' ['SLR']
* 'channel_exit_water_sediment~bedload__volume_fraction' ['f_bedload']
* 'channel_exit_water_sediment~suspended__mass_concentration' ['C0_percent']
* 'sea_water_surface__elevation' ['stage']
* 'sea_water__depth' ['depth']
* 'sea_bottom_surface__elevation' ['eta']
