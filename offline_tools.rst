######################
Offline curation tools
######################

.. _autotagger:

.. index::
   single: offline curation; autotagger
   single: autotagger

**********************************
Automated offline sequence tagging
**********************************
Sequence tagging is the process of identifying alleles by scanning the 
sequence bin linked to an isolate record. Loci need to be defined in an 
external sequence definition database that contains the sequences for known 
alleles. The tagging function uses BLAST to identify sequences and will tag 
the specific sequence region with locus information and an allele designation 
if a matching allele is identified by reference to an external database.

There is a script called 'autotag.pl' in the BIGSdb package. This can be used 
to tag genome sequences from the command line.

Before autotag.pl can be run for the first time, a log file needs to be 
created. This can be created if it doesn't already exist with the following: ::

  sudo touch /var/log/bigsdb_scripts.log
  sudo chown bigsdb /var/log/bigsdb_scripts.log

The autotag.pl script should be installed in /usr/local/bin. It is run as 
follows: ::

  autotag.pl --database <database configuration>

where <database configuration> is the name used for the argument 'db' when 
using the BIGSdb application.

If you have multiple processor cores available, use the --threads option to 
set the number of jobs to run in parallel.  Isolates for scanning will be split
among the threads.

The script must be run by a user that can both write to the log file and access
the databases, e.g. the 'bigsdb' user (see 'Setting up the offline job 
manager').

A full list of options can be found by typing: ::
  
 autotag.pl --help

 NAME
     autotag.pl - BIGSdb automated allele tagger

 SYNOPSIS
     autotag.pl --database NAME [options]

 OPTIONS
 -0, --missing
    Marks missing loci as provisional allele 0. Sets default word size to 15.
           
 -d, --database NAME
     Database configuration name.

 -h, --help
     This help page.

 -i, --isolates LIST  
     Comma-separated list of isolate ids to scan (ignored if -p used).
           
 -I, --exclude_isolates LIST
     Comma-separated list of isolate ids to ignore.

 -l, --loci LIST
     Comma-separated list of loci to scan (ignored if -s used).

 -L, --exclude_loci LIST
     Comma-separated list of loci to exclude

 -m, --min_size SIZE
     Minimum size of seqbin (bp) - limit search to isolates with at least this
     much sequence.
           
 -n, --new_only
     New (previously untagged) isolates only. Combine with --new_max_alleles
     if required.
     
 --new_max_alleles ALLELES
     Set the maximum number of alleles that can be designated or sequences
     tagged before an isolate is not considered new when using the --new_only
     option. 

 -o, --order
     Order so that isolates last tagged the longest time ago get scanned first
     (ignored if -r used).
           
 -p, --projects LIST
     Comma-separated list of project isolates to scan.

 -P, --exclude_projects LIST
     Comma-separated list of projects whose isolates will be excluded.
        
 -q, --quiet
     Only error messages displayed.

 -r, --random
     Shuffle order of isolate ids to scan.

 -R, --locus_regex REGEX
     Regex for locus names.

 -s, --schemes LIST
     Comma-separated list of scheme loci to scan.

 -t, --time MINS
     Stop after t minutes.

 --threads THREADS
     Maximum number of threads to use.

 -T, --already_tagged
     Scan even when sequence tagged (no designation).
     
 -v, --view VIEW
     Isolate database view (overrides value set in config.xml).

 -w, --word_size SIZE
     BLASTN word size.

 -x, --min ID
     Minimum isolate id.

 -y, --max ID
     Maximum isolate id.

.. _autodefiner:

.. index::
   single: offline curation; auto allele definer
   single: auto allele definer

***********************************
Automated offline allele definition
***********************************
There is a script called 'scannew.pl' in the BIGSdb scripts/automation 
directory. This can be used to identify new alleles from the command line. 
This can (optionally) upload these to a sequence definition database.

Before scannew.pl can be run for the first time, a log file needs to be 
created. This can be created if it doesn't already exist with the following: ::

  sudo touch /var/log/bigsdb_scripts.log
  sudo chown bigsdb /var/log/bigsdb_scripts.log

The autotag.pl script should be installed in /usr/local/bin. It is run as 
follows: ::

  scannew.pl --database <database configuration>

where <database configuration> is the name used for the argument 'db' when 
using the BIGSdb application.  

If you have multiple processor cores available, use the --threads option to 
set the number of jobs to run in parallel.  Loci for scanning will be split 
among the threads.

The script must be run by a user that can both write to the log file and access
the databases, e.g. the 'bigsdb' user (see 'Setting up the offline job 
manager').

A full list of options can be found by typing: ::

 scannew.pl --help

 NAME
   scannew.pl - BIGSdb automated allele definer

 SYNOPSIS
   scannew.pl --database NAME [options]

 OPTIONS
 -a, --assign
      Assign new alleles in definitions database.

 -A, --alignment INT
     Percentage alignment (default: 100).

 -B, --identity INT
     Percentage identity (default: 99).

 -c, --coding_sequences
     Only return complete coding sequences.

 -d, --database NAME
     Database configuration name.

 -h, --help
     This help page.

 -i, --isolates LIST
     Comma-separated list of isolate ids to scan (ignored if -p used).
           
 -I, --exclude_isolates LIST
     Comma-separated list of isolate ids to ignore.

 -l, --loci LIST
     Comma-separated list of loci to scan (ignored if -s used).

 -L, --exclude_loci LIST
     Comma-separated list of loci to exclude.

 -m, --min_size SIZE
     Minimum size of seqbin (bp) - limit search to isolates with at least this
     much sequence.
           
 -n, --new_only
     New (previously untagged) isolates only.

 -o, --order
     Order so that isolates last tagged the longest time ago get scanned first
     (ignored if -r used).
           
 -p, --projects LIST
     Comma-separated list of project isolates to scan.

 -P, --exclude_projects LIST
     Comma-separated list of projects whose isolates will be excluded.
           
 -r, --random
     Shuffle order of isolate ids to scan.

 -R, --locus_regex REGEX
     Regex for locus names.

 -s, --schemes LIST
     Comma-separated list of scheme loci to scan.

 -t, --time MINS
     Stop after t minutes.

 --threads THREADS
     Maximum number of threads to use.

 -T, --already_tagged
     Scan even when sequence tagged (no designation).
     
 -v, --view VIEW
     Isolate database view (overrides value set in config.xml).     

 -w, --word_size SIZE
     BLASTN word size.

 -x, --min ID
     Minimum isolate id.

 -y, --max ID
     Maximum isolate id.

.. index::
   pair: autotagger; stop
   pair: auto allele definer; stop

*************************************
Cleanly interrupting offline curation
*************************************
Sometimes you may wish to stop running autotagger or allele autodefiner jobs as
they can be run for a long time and as CRON jobs.  If these are running in 
single threaded mode, the easiest way is to simply send a kill signal to the 
process, i.e. identify the process id using 'top', e.g. 23232 and then ::

 kill 23232

The scripts should respond to this signal within a couple of seconds, clean up 
all their temporary files and write the history log (where appropriate).  Do 
not use 'kill -9' as this will terminate the processes immediately and not 
allow them to clean up.

If these scripts are running using multiple threads, then you need to cleanly 
kill each of these.  The simplest way to terminate all autotagger jobs is to, 
type ::

 pkill autotag

The parent process will wait for all forked processes to cleanly terminate and 
then exit itself.

Similarly, to terminate all allele autodefiner jobs, type ::

 pkill scannew

***************************************
Uploading contigs from the command line
***************************************
There is a script called upload_contigs.pl in the BIGSdb scripts/maintenance
directory.  This can be used to upload contigs from a local FASTA file for a
specified isolate record.

The upload_contigs.pl script should be installed in /usr/local/bin.  It is run
as follows: ::

 upload_contigs.pl --database <NAME> --isolate <ID> --file <FILE> 
     --curator <ID> --sender <ID> 

The script must be run by a user who has the appropriate database permissions
and the local configuration settings should be modified to match the database
user account to be used. The default setting uses the 'apache' user which is 
used by the BIGSdb web interface.

A full list of options can be found by typing: ::

 upload_contigs.pl --help   
 
 NAME
     upload_contigs.pl - Upload contigs to BIGSdb isolate database

 SYNOPSIS
     upload_contigs.pl --database NAME --isolate ID --file FILE 
          --curator ID --sender ID [options]

 OPTIONS
 -a, --append
     Upload contigs even if isolate already has sequences in the bin.
    
 -c, --curator ID  
     Curator id number. 
    
 -d, --database NAME
     Database configuration name.
    
 -f, --file FILE
     Full path and filename of contig file.

 -h, --help
     This help page.

 -i, --isolate ID  
     Isolate id of record to upload to.  
    
 -m, --method METHOD  
     Method, e.g. 'Illumina', default 'unknown'.  
    
 -s, --sender ID  
     Sender id number.        
     