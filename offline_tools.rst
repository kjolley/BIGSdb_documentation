######################
Offline curation tools
######################

**********************************
Automated offline sequence tagging
**********************************
Sequence tagging is the process of identifying alleles by scanning the sequence bin linked to an isolate record. Loci need to be defined in an external sequence definition database that contains the sequences for known alleles. The tagging function uses BLAST to identify sequences and will tag the specific sequence region with locus information and an allele designation if a matching allele is identified by reference to an external database.

There is a script called 'autotag.pl' in the BIGSdb package. This can be used to tag genome sequences from the command line.

Before autotag.pl can be run for the first time, a log file needs to be created. This can be created if it doesn't already exist with the following: ::

  sudo touch /var/log/bigsdb_scripts.log
  sudo chown bigsdb /var/log/bigsdb_scripts.log

The autotag.pl script should be installed in /usr/local/bin. It is run as follows: ::

  autotag.pl --database <database configuration>

where <database configuration> is the name used for the argument 'db' when using the BIGSdb application.

If you have multiple processor cores available, use the --threads option to set the number of jobs to run in parallel.  Isolates for scanning will be split among the threads.

The script must be run by a user that can both write to the log file and access the databases, e.g. the 'bigsdb' user (see 'Setting up the offline job manager').

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
     New (previously untagged) isolates only.

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

 -w, --word_size SIZE
     BLASTN word size.

 -x, --min ID
     Minimum isolate id.

 -y, --max ID
     Maximum isolate id.


***********************************
Automated offline allele definition
***********************************
There is a script called 'scannew.pl' in the BIGSdb scripts/automation directory. This can be used to identify new alleles from the command line. This can (optionally) upload these to a sequence definition database.

Before scannew.pl can be run for the first time, a log file needs to be created. This can be created if it doesn't already exist with the following: ::

  sudo touch /var/log/bigsdb_scripts.log
  sudo chown bigsdb /var/log/bigsdb_scripts.log

The autotag.pl script should be installed in /usr/local/bin. It is run as follows: ::

  scannew.pl --database <database configuration>

where <database configuration> is the name used for the argument 'db' when using the BIGSdb application.  

If you have multiple processor cores available, use the --threads option to set the number of jobs to run in parallel.  Loci for scanning will be split among the threads.

The script must be run by a user that can both write to the log file and access the databases, e.g. the 'bigsdb' user (see 'Setting up the offline job manager').

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

 -w, --word_size SIZE
     BLASTN word size.

 -x, --min ID
     Minimum isolate id.

 -y, --max ID
     Maximum isolate id.
