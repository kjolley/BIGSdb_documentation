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
* PostgreSQL database 9.5+
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

* `Archive::Zip <https://metacpan.org/pod/Archive::Zip>`_ - Used to upload to iTOL.
* `Bio::Biblio <https://metacpan.org/pod/Bio::Biblio>`_ - This used to be part of BioPerl but will need to be installed separately if using BioPerl 1.6.920 or later.
* `CGI <https://metacpan.org/pod/CGI>`_ - (version 4.04+) Common Gateway Interface requests and responses (used to be a core module but recently removed).
* `Config::Tiny <https://metacpan.org/pod/Config::Tiny>`_ - Configuration file handling.
* `Crypt::Eksblowfish::Bcrypt <https://metacpan.org/pod/Crypt::Eksblowfish::Bcrypt>`_ - Used for password hashing.
* `Data::Random <https://metacpan.org/pod/Data::Random>`_
* `Data::UUID <https://metacpan.org/pod/Data::UUID>`_ - Globally unique identifer handling for preference storage.
* `DBD::Pg <https://metacpan.org/pod/DBD::Pg>`_ - PostgreSQL database driver for DBI.
* `DBI <https://metacpan.org/pod/DBI>`_ - Database independent interface - module used to interact with databases.
* `Email::MIME <https://metacpan.org/pod/Email::MIME>`_ - Used to format E-mail messages.
* `Email::Sender <https://metacpan.org/pod/Email::Sender>`_ - Used to send E-mail messages by submission system.
* `Email::Valid <https://metacpan.org/pod/Email::Valid>`_ - Used to validate E-mails sent by job manager.
* `Excel::Writer::XLSX <https://metacpan.org/pod/Excel::Writer::XLSX>`_ - Used to export data in Excel format.
* `Exception::Class <https://metacpan.org/pod/Exception::Class>`_ - Exception handing.
* `IO::String <https://metacpan.org/pod/IO::String>`_
* `JSON <https://metacpan.org/pod/JSON>`_ - Used to manipulate JSON data.
* `List::MoreUtils <https://metacpan.org/pod/List::MoreUtils>`_ (version 0.28+).
* `Log::Dispatch::File <https://metacpan.org/pod/Log::Dispatch::File>`_ - Object for logging to file.
* `Log::Log4perl <https://metacpan.org/pod/Log::Log4perl>`_ - Configurable status and error logging.
* `LWP::UserAgent <https://metacpan.org/pod/LWP::UserAgent>`_ - Used to upload via API
* `Net::Oauth <https://metacpan.org/pod/Net::OAuth>`_ - Required for REST authentication (this needs to be installed even if you are not using REST).
* `Parallel::ForkManager <https://metacpan.org/pod/Parallel::ForkManager>`_ - Required for multi-threading tools and plugins.
* `Time::Duration <https://metacpan.org/pod/Time::Duration>`_ - Used by Job Viewer to display elapsed time in rounded units.
* `Try::Tiny <https://metacpan.org/pod/Try::Tiny>`_
* `XML::Parser::PerlSAX <https://metacpan.org/pod/XML::Parser::PerlSAX>`_ - part of libxml-perl - Used to parse XML configuration files.

Optional packages
=================
Installing these packages will enable extra functionality, but they are not required by the core BIGSdb package.

* ChartDirector (Perl) - library used for generating charts. 
  Used by some plugins.
* ImageMagick - mogrify used by some plugins.
* MAFFT 6.8+ - sequence alignment used by some plugins.
* Muscle - sequence alignment used by some plugins.
* Splitstree4 - used by GenomeComparator plugin.

