###################
BIGSdb dependencies
###################

*****************
Required packages
*****************
BIGSdb requires a number of software components to be installed:

Linux packages
==============
* Apache2 web server with mod_perl2
* PostgreSQL database
* Perl
* BioPerl
* BLAST+
* EMBOSS

  * infoalign - use to extract alignment stats in Genome Comparator.
  * sixpack - used to translate sequences in multiple reading frames.
  * stretcher - used for sequence alignment in allele query.

* Ipcress - part of exonerate package - used to simulate PCR reactions which can be used to filter the genome to predicted amplification products.
* Xvfb - X virtual framebuffer - needed to support SplitsTree in command line mode as used in Genome Comparator.

Perl modules
============
These are included with most Linux distributions.

* `DBI <http://search.cpan.org/~timb/DBI/DBI.pm>`_ - Database independent interface - module used to interact with databases.
* `DBD-Pg <http://search.cpan.org/~turnstep/DBD-Pg/Pg.pm>`_ - PostgreSQL database driver for DBI.
* `XML::Parser::perlSAX <http://search.cpan.org/~kmacleod/libxml-perl/lib/XML/Parser/PerlSAX.pm>`_ - part of libxml-perl - Used to parse XML configuration files.
* `Log::Log4perl <http://search.cpan.org/~mschilli/Log-Log4perl/lib/Log/Log4perl.pm>`_ - Configurable status and error logging.
* `Log::Dispatch::File <http://search.cpan.org/~drolsky/Log-Dispatch/lib/Log/Dispatch/File.pm>`_ - Object for logging to file.
* `Error <http://search.cpan.org/~shlomif/Error/lib/Error.pm>`_ - Exception handling.
* `Config::Tiny <http://search.cpan.org/~rsavage/Config-Tiny/lib/Config/Tiny.pm>`_ - Configuration file handling.
* `Bio::Biblio <http://search.cpan.org/~cdraug/Bio-Biblio/lib/Bio/Biblio.pm>`_ - This used to be part of BioPerl but will need to be installed separately if using BioPerl 1.6.920 or later.
* `IO::String <http://search.cpan.org/~gaas/IO-String/String.pm>`_
* `Data::UUID <http://search.cpan.org/~rjbs/Data-UUID/UUID.pm>`_ - Globally unique identifer handling for preference storage.
* `List::MoreUtils <http://search.cpan.org/~adamk/List-MoreUtils/lib/List/MoreUtils.pm>`_ (version 0.28+).
* `Time::Duration <http://search.cpan.org/~avif/Time-Duration/Duration.pm>`_ [optional] - Used by Job Viewer to display elapsed time in rounded units.
* `Excel::Writer::XLSX <http://search.cpan.org/~jmcnamara/Excel-Writer-XLSX/lib/Excel/Writer/XLSX.pm>`_ - Used to export data in Excel format.
* `Parallel::ForkManager <http://search.cpan.org/~szabgab/Parallel-ForkManager/lib/Parallel/ForkManager.pm>`_ - Required for multi-threading autotagger and autodefiner scripts.

Optional packages
=================
Installing these packages will enable extra functionality, but they are not required by the core BIGSdb package.

* ChartDirector - library used for generating charts. Used by some plugins.
* ImageMagick - mogrify used by some plugins.
* MAFFT - sequence alignment used by some plugins.
* Muscle - sequence alignment used by some plugins.
* Splitstree4 - used by GenomeComparator plugin.

