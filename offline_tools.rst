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
    
 -e, --exemplar
     Only use alleles with the 'exemplar' flag set in BLAST searches to identify
     locus within genome. Specific allele is then identified using a database 
     lookup. This may be quicker than using all alleles for the BLAST search, 
     but will be at the expense of sensitivity. If no exemplar alleles are set 
     for a locus then all alleles will be used. Sets default word size to 15.

 -f --fast
     Perform single BLAST query against all selected loci together. This will
     take longer to return any results but the overall scan should finish 
     quicker. This method will also use more memory - this can be used with
     --exemplar to mitigate against this.

 -h, --help
     This help page.

 -i, --isolates LIST  
     Comma-separated list of isolate ids to scan (ignored if -p used).
    
 --isolate_list_file FILE  
     File containing list of isolate ids (ignored if -i or -p used).
           
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
     New (previously untagged) isolates only.  Combine with --new_max_alleles
     if required.
    
 --new_max_alleles ALLELES
     Set the maximum number of alleles that can be designated or sequences
     tagged before an isolate is not considered new when using the --new_only
     option.    

 -o, --order
     Order so that isolates last tagged the longest time ago get scanned first
     (ignored if -r used).
    
 --only_already_tagged
     Only check loci that already have a tag present (but no allele designation).
     This must be combined with the --already_tagged option or no loci will
     match. This option is used to perform a catch-up scan where a curator has
     previously tagged sequence regions prior to alleles being defined, without
     the need to scan all missing loci.
           
 -p, --projects LIST
     Comma-separated list of project isolates to scan.

 -P, --exclude_projects LIST
     Comma-separated list of projects whose isolates will be excluded.
        
 -q, --quiet
     Only error messages displayed.

 -r, --random
     Shuffle order of isolate ids to scan.
     
 --reuse_blast
     Reuse the BLAST database for every isolate (when running --fast option). 
     All loci will be scanned rather than just those missing from an isolate. 
     Consequently, this may be slower if isolates have already been scanned, 
     and for the first isolate scanned by a thread. On larger schemes, such as 
     wgMLST, or when isolates have not been previously scanned, setting up the
     BLAST database can take a significant amount of time, so this may be 
     quicker. This option is always selected if --new_only is used.

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

.. _defining_exemplars:

.. index::
   pair: exemplar alleles; defining

*************************
Defining exemplar alleles
*************************
Exemplar alleles are a subset of the total number of alleles defined for a
locus that encompass the known diversity within a specified identity threshold.
They can be used to speed up :ref:`autotagging<autotagger>` as the BLAST 
queries are performed against exemplars to identify the locus region in the 
genome followed by a direct database lookup of the sequence found to identify 
the exact allele found. This is usually combined with the autotagger --fast 
option.

There is a script called 'find_exemplars.pl' in the BIGSdb scripts/maintenance
directory. 

A full list of options can be found by typing: ::

 find_exemplars.pl --help
 
 NAME
     find_exemplars.pl - Identify and mark exemplar alleles for use
     by tagging functions

 SYNOPSIS
     find_exemplars.pl --database NAME   [options]

 OPTIONS

 --database NAME
     Database configuration name.
    
 --datatype DNA|peptide
     Only define exemplars for specified data type (DNA or peptide)    
   
 --exclude_loci LIST
     Comma-separated list of loci to exclude
    
 --help
     This help page.
    
 --loci LIST
     Comma-separated list of loci to scan (ignored if -s used).
  
 --locus_regex REGEX
     Regex for locus names.
    
 --schemes LIST
     Comma-separated list of scheme loci to scan.
    
 --update
     Update exemplar flags in database.
    
 --variation IDENTITY
     Value for percentage identity variation that exemplar alleles
     cover (smaller value will result in more exemplars). Default: 10. 

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
      
 --allow_frameshift
     Allow sequences to contain a frameshift so that the length is not a 
     multiple of 3, or an internal stop codon. To be used with 
     --coding_sequences option to allow automated curation of pseudogenes.
     New alleles assigned will be flagged either 'frameshift' or 'internal stop
     codon' if appropriate.  Essentially, combining these two options only 
     checks that the sequence starts with a start codon and ends with a stop
     codon.   

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
     
 --isolate_list_file FILE  
     File containing list of isolate ids (ignored if -i or -p used).
           
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
     
 --type_alleles
     Only use alleles with the 'type_allele' flag set to identify locus.
     If a partial match is found then a full database lookup will be performed
     to identify any known alleles. Using this option will constrain the search
     space so that allele definitions don't become more variable over time. Note
     that you must have at least one allele defined as a type allele for a locus
     if you use this option otherwise you will not find any matches!

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
kill each of these.  The simplest way to terminate all autotagger jobs is to 
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
     
 --min_length LENGTH
     Exclude contigs with length less than value.
    
 -s, --sender ID  
     Sender id number.        
     