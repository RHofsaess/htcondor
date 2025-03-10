Stable Release Series 9.0
=========================

This is the stable release series of HTCondor. As usual, only bug fixes
(and potentially, ports to new platforms) will be provided in future
9.0.x releases. New features will be added in the 9.1.x development
series.

The details of each version are described below.

Version 9.0.6
-------------

Release Notes:

.. HTCondor version 9.0.6 released on Month Date, 2021.

- HTCondor version 9.0.6 not yet released.

New Features:

- None.

Bugs Fixed:

- None.

Version 9.0.5
-------------

Release Notes:

.. HTCondor version 9.0.5 released on Month Date, 2021.

- HTCondor version 9.0.5 not yet released.

New Features:

- If the SCITOKENS authentication method succeeds (that is, the client
  presented a valid SciToken) but the user-mapping fails, HTCondor will
  try the next authentication method in the list instead of failing.
  :jira:`589`

Bugs Fixed:

- Fixed a bug where ``condor_gpu_discovery`` would not report any GPUs if
  any MIG-enabled GPU on the system were configured in certain ways.  Fixed
  a bug which could cause ``condor_gpu_discovery``'s output to become
  unparseable after certain errors.
  :jira:`476`

- Fixed a bug where jobs running on Linux machines with cgroups enabled
  would not count files created in /dev/shm in the MemoryUsage attribute.
  :jira:`586`

- Fixed a bug where running *condor_who* as a non-root user on a Unix
  system would print a confusing warning to stderr about running as
  non-root.
  :jira:`590`

- Fixed a bug on the Windows platform where *condor_submit* would crash
  rarely after succesfully submitting a job.  This caused problems for programs
  that look at the return status of *condor_submit*, including *condor_dagman*
  :jira:`579`

- HTCondor no longer ignores files in a job's spool directory if they happen
  to share a name with an entry in ``transfer_input_files``.  This allows
  jobs to specify the same file in ``transfer_input_files`` and in
  ``transfer_checkpoint_files``, and still resume properly after a checkpoint.
  :jira:`583`

- The job attribute ``ExitCode`` is no longer missing from the job ad after
  ``OxExitHold`` triggers.
  :jira:`599`

- Fixed a bug in the *condor_now* tool, where the *condor_schedd* would
  not use an existing security session to run the selected job on the
  claimed resources.
  This could often lead to the job being unable to start.
  :jira:`603`


Version 9.0.4
-------------

Release Notes:

-  HTCondor version 9.0.4 released on July 29, 2021.

New Features:

-  None.

Bugs Fixed:

-  *Security Item*: This release of HTCondor fixes a security-related bug
   described at

   -  `http://htcondor.org/security/vulnerabilities/HTCONDOR-2021-0003.html <http://htcondor.org/security/vulnerabilities/HTCONDOR-2021-0003.html>`_.
   -  `http://htcondor.org/security/vulnerabilities/HTCONDOR-2021-0004.html <http://htcondor.org/security/vulnerabilities/HTCONDOR-2021-0004.html>`_.

   :jira:`509`
   :jira:`587`


Version 9.0.3
-------------

Release Notes:

-  HTCondor version 9.0.3 released on July 27, 2021 and pulled two days later when an issue was found with a patch.

New Features:

-  None.

Bugs Fixed:

-  None.

Version 9.0.2
-------------

Release Notes:

- HTCondor version 9.0.2 released on July 8, 2021.

- Removed support for GRAM grid jobs.
  :jira:`561`

New Features:

- HTCondor can now be configured to only use FIPS 140-2 approved security
  functions by using the new configuration template: ``use security:FIPS``.
  :jira:`319`

- Added new command-line flag to `condor_gpu_discovery`, ``-divide``,
  which functions like ``-repeat``, except that it divides the GPU attribute
  ``GlobalMemoryMb`` by the number of repeats (and adds the GPU
  attribute ``DeviceMemoryMb``, which is the undivided total).  To enable
  this new behavior, modify ``GPU_DISCOVERY_EXTRA`` appropriately.
  :jira:`454`

- The maximum line length for ``STARTD_CRON`` and ``SCHEDD_CRON`` job output
  has been extended from 8k bytes to 64k bytes.
  :jira:`498`

- Added two new commands to *condor_submit* - ``use_scitokens`` and ``scitokens_file``.
  :jira:`508`

- Reduced `condor_shadow` memory usage by 40% or more on machines with many
  (more than 64) cores.  This allows a correspondingly greater number of shadows and thus
  jobs to run on these submit machines.
  :jira:`540`

- Added support for using an authenticated SMTP relay on port 587 to
  condor_mail.exe on Windows.
  :jira:`303`

- The `condor_job_router_info` tool will now show info for a rootly JobRouter
  even when the tool is not running as root.  This change affects the way
  jobs are matched when using the ``-match`` or ``-route`` options.
  :jira:`525`

- *condor_gpu_discovery* now recognizes Capability 8.6 devices and reports the
  correct number of cores per Compute Unit.
  :jira:`544`

- Added command line option ``--copy-ssh-key`` to *bosco_cluster*. When set
  to `no`, this option prevents *bosco_cluster* from installing an ssh
  key on the remote system, and assume passwordless ssh is already
  possible.
  :jira:`270`

- Update to be able to link in scitokens-cpp library directly, rather than
  always using dlopen(). This allows SciTokens to be used with the conda-forge
  build of HTCondor.
  :jira:`541`

Bugs Fixed:

- When a Singularity container is started, and the test is run before the job,
  and the test fails, the job is now put back to idle instead of held.
  :jira:`539`

- Fixed Munge authentication, which was broken starting with HTCondor 8.9.9.
  :jira:`378`

- Fixed a bug in the Windows MSI installer where installation would only succeed
  at the default location of ``C:\Condor``.
  :jira:`543`

- Fixed a bug that prevented docker universe jobs from running on machines
  whose hostnames were longer than about 60 characters.
  :jira:`473`

- Fixed a bug that prevented *bosco_cluster* from detecting the remote host's
  platform when it is running Scientific Linux 7.
  :jira:`503`

- Fixed a bug that caused the ``query-krb`` and ``delete-krb`` options of *condor_store_cred*
  to fail.  This bug also affected the Python bindings ``query_user_cred`` and ``delete_user_cred``
  methods
  :jira:`533`

- Attribute ``GridJobId`` is no longer removed from the job ad of grid-type
  ``batch`` jobs when the job enters ``Completed`` or ``Removed`` status.
  :jira:`534`

- Fixed a bug that could prevent HTCondor from noticing new events in job
  event logs, if those logs were being written from one machine and read
  from another via AFS.
  :jira:`463`

- Using expressions for values in the ads of grid universe jobs of type
  `batch` now works correctly.
  :jira:`507`

- Fixed a bug that prevented a  personal condor from running in a private
  user namespace.
  :jira:`550`

- Fixed a bug in the *condor_who* program that caused it to hang on Linux
  systems, especially those running AFS or other shared filesystems.
  :jira:`530`
  :jira:`573`

- Fixed a bug that cause the *condor_master* to hang for up to two minutes
  when shutting down, if it was configured to be a personal condor.
  :jira:`548`

- When a grid universe job of type ``nordugrid`` fails on the remote system,
  the local job is now put on hold, instead of automatically resubmitted.
  :jira:`535`

- Fixed a bug that caused SSL authentication to crash on rare occasions.
  :jira:`428`

- Added the missing Ceiling attribute to negotiator user priorities in the
  Python bindings.
  :jira:`560`

- Fixed a bug in DAGMan where `SUBMIT-DESCRIPTION` statements were incorrectly
  logging duplicate description warnings.
  :jira:`511`

- Add the libltdl library to the HTCondor tarball. This library was
  inadvertently omitted when streamlining the build process in version 8.9.12.
  :jira:`576`


Version 9.0.1
-------------

Release Notes:

- HTCondor version 9.0.1 released on May 17, 2021.

- The installer for Windows will now replace the ``condor_config``
  file even on an update.  You must use ``condor_config.local`` or
  a configuration directory to customize the configuration if you wish
  to preserve configuration changes across updates.

Known Issues:

- There is a known issue with the installer for Windows where it does
  not honor the Administrator Access list set in the MSI permissions
  dialog on a fresh install.  Instead it will always set the
  Administrator access to the default value.

- MUNGE security is temporarily broken.

New Features:

- The Windows MSI installer now sets up user-based authentication and creates 
  an IDTOKEN for local administration.
  :jira:`407`

- When the ``AssignAccountingGroup`` configuration template is in effect
  and a user submits a job with a requested accounting group that they are not
  permitted to use, the submit will be rejected with an error message.
  This configuration template has a new optional second argument that can be used
  to quietly ignore the requested accounting group instead.
  :jira:`426`

- Added the OpenBLAS environment variable ``OPENBLAS_NUM_THREADS`` to the list
  of environment variables exported by the *condor_starter* per these
  `recommendations <https://github.com/xianyi/OpenBLAS/wiki/faq#how-can-i-use-openblas-in-multi-threaded-applications>`_.
  :jira:`444`

- HTCondor now parses ``/usr/share/condor/config.d/`` for configuration before
  ``/etc/condor/config.d``, so that packagers have a convenient place to adjust
  the HTCondor configuration.
  :jira:`45`

- Added a boolean option ``LOCAL_CREDMON_TOKEN_USE_JSON`` for the local issuer
  *condor_credmon_oauth* that is used to decide whether or not the bare token
  string in a generated access token file is wrapped in JSON. Default is
  ``LOCAL_CREDMON_TOKEN_USE_JSON = true`` (wrap token in JSON).
  :jira:`367`

Bugs Fixed:

- Fixed a bug where sending an updated proxy to an execute node could
  cause the *condor_starter* to segfault when AES encryption was enabled
  (which is the default).
  :jira:`456`
  :jira:`490`

- Fixed a bug with jobs that require running on a different machine
  after a failure by referring to MachineAttrX attributes in their
  requirements expression.
  :jira:`434`

- Fixed a bug in the way ``AutoClusterAttrs`` was calculated that could
  cause matchmaking to ignore attributes changed by ``job_machine_attrs``.
  :jira:`414`

- Fixed a bug in the implementation of the submit commands ``max_retries``
  and ``success_exit_code`` which would cause jobs which exited on a
  signal to go on hold (instead of exiting or being retried).
  :jira:`430`

- Fixed a memory leak in the job router, usually triggered when job
  policy expressions cause removal of the job.
  :jira:`408`

- Fixed some bugs that caused ``bosco_cluster --add`` to fail.
  Allow ``remote_gahp`` to work with older Bosco installations via
  the ``--rgahp-script`` option.
  Fixed security authorization failure between *condor_gridmanager*
  and *condor_ft-gahp*.
  :jira:`433`
  :jira:`438`
  :jira:`451`
  :jira:`452`
  :jira:`487`

- Fixed a bug in *condor_submit* when a ``SEC_CREDENTIAL_PRODUCER`` was
  configured that could result in *condor_submit* reporting that the
  Queue statement of a submit file was missing or invalid.
  :jira:`427`

- Fixed a bug in the local issuer *condor_credmon_oauth* where SciTokens version
  2.0 tokens were being generated without an "aud" claim. The "aud" claim is now
  set to ``LOCAL_ISSUER_TOKEN_AUDIENCE``. The "ver" claim can be changed from
  the default of "scitokens:2.0" by setting ``LOCAL_ISSUER_TOKEN_VERSION``.
  :jira:`445`

- Fixed several bugs that could result in the *condor_token_* tools aborting with
  a c++ runtime error on newer versions of Linux.
  :jira:`449`

Version 9.0.0
-------------

Release Notes:

- HTCondor version 9.0.0 released on April 14, 2021.

- The installer for Windows platforms was not ready for 9.0.0.
  Windows support will appear in 9.0.1.

- Removed support for CREAM and Unicore grid jobs, glexec privilege separation, DRMAA, and *condor_cod*.

Known Issues:

- MUNGE security is temporarily broken.

- The *bosco_cluster* command is temporarily broken.

New Features:

- A new tool *condor_check_config* can be used after an upgrade when you had a working
  condor configuration before the upgrade. It will report configuration values that should be changed.
  In this version the tool for a few things related to the change to a more secure configuration by default.
  :jira:`384`

- The *condor_gpu_discovery* tool now defaults to using ``-short-uuid`` form for GPU ids on machines
  where the CUDA driver library has support for them. A new option ``-by-index`` has been added
  to select index-based GPU ids.
  :jira:`145`

Bugs Fixed:

- Fixed a bug introduced in 8.9.12 where the condor_job_router inside a CE would crash when
  evaluating periodic expressions
  :jira:`402`
