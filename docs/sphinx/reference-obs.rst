Libobs API Reference
====================

.. function:: bool obs_startup(const char *locale, const char *module_config_path, profiler_name_store_t *store)

   Initializes Libobs.
  
   :param  locale:             The locale to use for modules
                               (E.G. "en-US")
   :param  module_config_path: Path to module config storage directory
                               (or NULL if none)
   :param  store:              The profiler name store for OBS to use or NULL

.. function:: void obs_shutdown(void)

   Releases all data associated with OBS and terminates the OBS context

.. function:: bool obs_initialized(void)

   :return: true if the main OBS context has been initialized

.. function:: uint32_t obs_get_version(void)

   :return: The current core version

.. function:: const char *obs_get_version_string(void)

   :return: The current core version string

.. function:: void obs_set_locale(const char *locale)

   Sets a new locale to use for modules.  This will call
   obs_module_set_locale for each module with the new locale.
  
   :param  locale: The locale to use for modules

.. function:: const char *obs_get_locale(void)

   :return: The current locale

.. function:: profiler_name_store_t *obs_get_profiler_name_store(void)

   :return: the profiler name store (see util/profiler.h) used by OBS,
   which is either a name store passed to obs_startup, an internal name
   store, or NULL in case obs_initialized() returns false.

.. function:: int obs_reset_video(struct obs_video_info *ovi)

   Sets base video output base resolution/fps/format.
  
   Note: This data cannot be changed if an output is currently active.
   Note: The graphics module cannot be changed without fully destroying the
         OBS context.
  
   :param   ovi: Pointer to an obs_video_info structure containing the
                 specification of the graphics subsystem,
   :return:      | OBS_VIDEO_SUCCESS if successful
                 | OBS_VIDEO_NOT_SUPPORTED if the adapter lacks capabilities
                 | OBS_VIDEO_INVALID_PARAM if a parameter is invalid
                 | OBS_VIDEO_CURRENTLY_ACTIVE if video is currently active
                 | OBS_VIDEO_MODULE_NOT_FOUND if the graphics module is not found
                 | OBS_VIDEO_FAIL for generic failure

.. function:: bool obs_reset_audio(const struct obs_audio_info *oai)

   Sets base audio output format/channels/samples/etc
  
   Note: Cannot reset base audio if an output is currently active.

.. function:: bool obs_get_video_info(struct obs_video_info *ovi)

   Gets the current video settings, returns false if no video

.. function:: bool obs_get_audio_info(struct obs_audio_info *oai)

   Gets the current audio settings, returns false if no audio

.. function:: int obs_open_module(obs_module_t **module, const char *path, const char *data_path)

   Opens a plugin module directly from a specific path.
  
   If the module already exists then the function will return successful, and
   the module parameter will be given the pointer to the existing module.
  
   This does not initialize the module, it only loads the module image.  To
   initialize the module, call obs_init_module.
  
   :param  module:    The pointer to the created module.
   :param  path:      Specifies the path to the module library file.  If the
                      extension is not specified, it will use the extension
                      appropriate to the operating system.
   :param  data_path: Specifies the path to the directory where the module's
                      data files are stored (or NULL if none)
   :returns:          | MODULE_SUCCESS if successful
                      | MODULE_ERROR if a generic error occurred
                      | MODULE_FILE_NOT_FOUND if the module was not found
                      | MODULE_MISSING_EXPORTS if required exports are missing
                      | MODULE_INCOMPATIBLE_VER if incompatible version

.. function:: bool obs_init_module(obs_module_t *module)

   Initializes the module, which calls its obs_module_load export.  If the
   module is already loaded, then this function does nothing and returns
   successful.

.. function:: void obs_log_loaded_modules(void)

   Logs loaded modules

.. function:: const char *obs_get_module_file_name(obs_module_t *module)

   Returns the module file name

.. function:: const char *obs_get_module_name(obs_module_t *module)

   Returns the module full name (or NULL if none)

.. function:: obs_get_module_author(obs_module_t *module)

   Returns the module author(s)

.. function:: const char *obs_get_module_description(obs_module_t *module)

   Returns the module description

.. function:: const char *obs_get_module_binary_path(obs_module_t *module)

   Returns the module binary path

.. function:: const char *obs_get_module_data_path(obs_module_t *module)

   Returns the module data path

.. function:: void obs_add_module_path(const char *bin, const char *data)

   Adds a module search path to be used with obs_find_modules.  If the search
   path strings contain %module%, that text will be replaced with the module
   name when used.
  
   :param  bin:  Specifies the module's binary directory search path.
   :param  data: Specifies the module's data directory search path.

.. function:: void obs_load_all_modules(void)

   Automatically loads all modules from module paths (convenience function)

.. function:: void obs_post_load_modules(void)

   Notifies modules that all modules have been loaded.

.. type:: struct obs_module_info
.. member:: const char *obs_module_info.bin_path
.. member:: const char *obs_module_info.data_path

