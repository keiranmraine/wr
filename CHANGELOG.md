# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/) and this
project adheres to [Semantic Versioning](http://semver.org/).


## [0.5.0] - 2017-01-26
### Added
- `wr cloud deploy` now has options for setting your network CIDR, gateway IP,
  DNS name servers and minimum disk size.
- `wr add` command-specific options now allow specifying environment variable
  overrides.

### Fixed
- Manager's IP is now calculated correctly on hosts with multiple network
  interfaces.
- `wr cloud deploy` applies appropriate private permissions to the ssh key file
  it copies over to the "head" node.
- Numerous fixes made to OpenStack scheduler, allowing it to work as expected
  with multi-core flavors and not overload the system by spawning new servers
  sequentially.

### Changed
- Using `wr add` with a remote manager now no longer associates local
  environment variables with the command; commands run with the remote variables
  instead.
- Memory requirements are no longer increased by 100MB unless the resulting
  figure would be less than 1GB.
- Backwards incompatible internal API changes for the jobqueue package.


## [0.4.0] - 2017-01-19
### Added
- `wr add --disk` causes the creation of suitable sized temporary volumes when
  using the OpenStack scheduler, if necessary.
- New `wr add` command-specific options now allow specifying which cloud OS
  image to use to run that command.

### Fixed
- Improved error message if an invalid OS image name prefix is supplied.

### Changed
- Format of file taken by `wr add -f` has changed completely; read the help.
- Backwards incompatible internal API changes for the cloud package.


## [0.3.1] - 2016-12-16
### Fixed
- `wr cloud deploy` now creates working ssh tunnels for typical ssh configs.


## [0.3.0] - 2016-12-12
### Added
- Added commands can now be dependent on previously added commands, using
  arbitrary and multiple dependency groups for "live" dependencies.
- Status web page now shows dependency information.

### Fixed
- Updated help text to note what is not implemented yet.

### Changed
- Format of file taken by `wr add -f` now has an additional column for
  specifying dependency group-based dependencies, which changes the column
  order. Old files that had dependencies specified are no longer compatible!


## [0.2.0] - 2016-12-06
### Added
- Added commands can now be dependent on previously added commands.
- Status web page now has a favicon.
- `wr cloud deploy` (and `wr manager start`) now take options to limit what
  cloud flavors can be used, and to specify a post-creation script.
- Manager now has improved logging of a variety of errors.

### Fixed
- Status web page now correctly sorts the RepGroups.
- Status web page progress bars no longer get stuck in 'ready' state, even when
  complete.
- Status web page progress bars no longer flicker.
- Manager works with latest versions of OpenStack (which do not generate DER
  format SSH private keys).
- Manager running on OpenStack no longer stops spawning new servers when it
  should.

### Changed
- Format of file taken by `wr add -f` now had additional columns for specifying
  dependencies.
- Status web page no longer shows the unimplemented search box.
- Status web page now show deleted commands as deleted instead of complete.


## [0.1.1] - 2016-10-21
### Added
- `wr cloud deploy -h` now includes additional help text to explain OpenStack
  usage.
- `wr add` now has a `--retries` option, letting you choose how many automatic
  retries failed commands undergo before user action is required.
- Makefile now specifies a 'report' action to do most of goreportcard.

### Fixed
- `wr cloud deploy` now uses the --os_ram value for the initial "head" node.
- `wr status` now shows the status of currently running commands.
- Mistakes in typing a `wr` command no longer duplicate the error message.
- Test timings relaxed to hopefully pass in Travis more reliably.

### Changed
- The release zip uploaded to github has a better architecture name (x86-64
  instead of amd64).
- Removed the unused deploypidfile config option.
- Removed the unused ssh package.


## [0.1.0] - 2016-10-14
### Added
- First release of wr
- No workflow implementation
- Adding and automated running of commands
- Run commands on local machine, via LSF, or via OpenStack
