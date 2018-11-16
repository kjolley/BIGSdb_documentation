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
* Perl 5.10+
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

* `Archive::Zip <http://search.cpan.org/~phred/Archive-Zip/>`_ - [required by PhyloTree plugin] - Used to upload to iTOL
* `Bio::Biblio <http://search.cpan.org/~cdraug/Bio-Biblio/lib/Bio/Biblio.pm>`_ - This used to be part of BioPerl but will need to be installed separately if using BioPerl 1.6.920 or later.
* `CGI <http://search.cpan.org/dist/CGI/>`_ - Common Gateway Interface requests and responses (used to be a core module but recently removed).
* `Config::Tiny <http://search.cpan.org/~rsavage/Config-Tiny/lib/Config/Tiny.pm>`_ - Configuration file handling.
* `Crypt::Eksblowfish::Bcrypt <http://search.cpan.org/~zefram/Crypt-Eksblowfish/lib/Crypt/Eksblowfish/Bcrypt.pm>`_ - Used for password hashing.
* `Data::Random <https://metacpan.org/pod/Data::Random>`_
* `Data::UUID <http://search.cpan.org/~rjbs/Data-UUID/UUID.pm>`_ - Globally unique identifer handling for preference storage.
* `DBD-Pg <http://search.cpan.org/~turnstep/DBD-Pg/Pg.pm>`_ - PostgreSQL database driver for DBI.
* `DBI <http://search.cpan.org/~timb/DBI/DBI.pm>`_ - Database independent interface - module used to interact with databases.
* `Email::MIME <http://search.cpan.org/~rjbs/Email-MIME/lib/Email/MIME.pm>`_ - Used to format E-mail messages.
* `Email::Sender <http://search.cpan.org/~rjbs/Email-Sender/lib/Email/Sender.pm>`_ - Used to send E-mail messages by submission system.
* `Email::Valid <http://search.cpan.org/~rjbs/Email-Valid/lib/Email/Valid.pm>`_ - Used to validate E-mails sent by job manager.
* `Excel::Writer::XLSX <http://search.cpan.org/~jmcnamara/Excel-Writer-XLSX/lib/Excel/Writer/XLSX.pm>`_ - Used to export data in Excel format.
* `Exception::Class <https://metacpan.org/pod/Exception::Class>`_ - Exception handing.
* `IO::String <http://search.cpan.org/~gaas/IO-String/String.pm>`_
* `JSON <http://search.cpan.org/~makamaka/JSON/>`_ - Used to manipulate JSON data.
* `List::MoreUtils <http://search.cpan.org/~adamk/List-MoreUtils/lib/List/MoreUtils.pm>`_ (version 0.28+).
* `Log::Dispatch::File <http://search.cpan.org/~drolsky/Log-Dispatch/lib/Log/Dispatch/File.pm>`_ - Object for logging to file.
* `Log::Log4perl <http://search.cpan.org/~mschilli/Log-Log4perl/lib/Log/Log4perl.pm>`_ - Configurable status and error logging.
* `LWP::UserAgent <http://search.cpan.org/~ether/libwww-perl/>`_ - [required by PhyloViz and PhyloTree plugins] - Used to upload via API
* `Net::Oauth <http://search.cpan.org/dist/Net-OAuth/lib/Net/OAuth.pm>`_ - Required for REST authentication (this needs to be installed even if you are not using REST).
* `Parallel::ForkManager <http://search.cpan.org/~yanick/Parallel-ForkManager/lib/Parallel/ForkManager.pm>`_ - Required for multi-threading tools and plugins.
* `Time::Duration <http://search.cpan.org/~avif/Time-Duration/Duration.pm>`_ [optional] - Used by Job Viewer to display elapsed time in rounded units.
* `Try::Tiny <https://metacpan.org/pod/Try::Tiny>`_
* `XML::Parser::perlSAX <http://search.cpan.org/~kmacleod/libxml-perl/lib/XML/Parser/PerlSAX.pm>`_ - part of libxml-perl - Used to parse XML configuration files.

Optional packages
=================
Installing these packages will enable extra functionality, but they are not required by the core BIGSdb package.

* ChartDirector (Perl) - library used for generating charts. 
  Used by some plugins.
* ImageMagick - mogrify used by some plugins.
* MAFFT 6.8+ - sequence alignment used by some plugins.
* Muscle - sequence alignment used by some plugins.
* Splitstree4 - used by GenomeComparator plugin.

