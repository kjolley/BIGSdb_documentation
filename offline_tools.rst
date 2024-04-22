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
   --already_tagged, -T
       Scan even when sequence tagged (no designation).
       
   --curator CURATOR ID
       Curator id to use for updates. By default -1 is used - there should be an
       autotagger account set with this id number.
              
   --database, -d NAME
       Database configuration name.
       
   --exclude_isolates, -I LIST
       Comma-separated list of isolate ids to ignore.
       
   --exclude_loci, -L LIST
       Comma-separated list of loci to exclude
       
   --exclude_projects, -P LIST
       Comma-separated list of projects whose isolates will be excluded.
       
   --exemplar, -e
       Only use alleles with the 'exemplar' flag set in BLAST searches to identify
       locus within genome. Specific allele is then identified using a database 
       lookup. This may be quicker than using all alleles for the BLAST search, 
       but will be at the expense of sensitivity. If no exemplar alleles are set 
       for a locus then all alleles will be used. Sets default word size to 15.
       
   --fast, -f
       Perform single BLAST query against all selected loci together. This will
       take longer to return any results but the overall scan should finish 
       quicker. This method will also use more memory - this can be used with
       --exemplar to mitigate against this.
   
   --help, -h
       This help page.
   
   --isolates, -i LIST  
       Comma-separated list of isolate ids to scan (ignored if -p used).
       
   --isolate_list_file FILE  
       File containing list of isolate ids (ignored if -i or -p used).
              
   --loci, -l LIST
       Comma-separated list of loci to scan (ignored if -s used).
       
   --locus_regex -R REGEX
       Regex for locus names.
    
   --max, -y ID
       Maximum isolate id.   
   
   --min, -x ID
       Minimum isolate id.
   
   --min_size, -m SIZE
       Minimum size of seqbin (bp) - limit search to isolates with at least this
       much sequence.
       
   --missing, -0
       Marks missing loci as provisional allele 0. Sets default word size to 15.
       
   --missing_alignment PERCENTAGE
       Minimum alignment threshold to use when tagging missing loci (default 30)
       
   --missing_identity PERCENTAGE
       Minimum identity threshold to use when tagging missing loci (default 50)  
       
   --new_max_alleles ALLELES
       Set the maximum number of alleles that can be designated or sequences
       tagged before an isolate is not considered new when using the --new_only
       option.   
              
   --new_only, -n
       New (previously untagged) isolates only.  Combine with --new_max_alleles
       if required.  
       
   --only_already_tagged
       Only check loci that already have a tag present (but no allele designation).
       This must be combined with the --already_tagged option or no loci will
       match. This option is used to perform a catch-up scan where a curator has
       previously tagged sequence regions prior to alleles being defined, without
       the need to scan all missing loci.
       
   --order, -o
       Order so that isolates last tagged the longest time ago get scanned first.
              
   --projects, -p LIST
       Comma-separated list of project isolates to scan.
          
   --quiet, -q
       Only error messages displayed.
       
   --reuse_blast
       Reuse the BLAST database for every isolate (when running --fast option). 
       All loci will be scanned rather than just those missing from an isolate. 
       Consequently, this may be slower if isolates have already been scanned, 
       and for the first isolate scanned by a thread. On larger schemes, such as 
       wgMLST, or when isolates have not been previously scanned, setting up the
       BLAST database can take a significant amount of time, so this may be 
       quicker. This option is always selected if --new_only is used.
   
   --schemes, -s LIST
       Comma-separated list of scheme loci to scan.
       
   --seqbin_reldate DAYS
       Filter to only include isolates for which the sequence bin was last
       modified within the specified number of days (set 1 for today).
       
   --threads THREADS
       Maximum number of threads to use.
   
   --time, -t MINS
       Stop after t minutes.
       
   --type_alleles
       Only use alleles with the 'type_allele' flag set to identify locus.
       Note that this is only used when combined with the --missing (-0) flag.
       You must have at least one allele defined as a type allele for a locus
       if you use this option otherwise you will not find any matches!
       
   --view, -v VIEW
       Isolate database view (overrides value set in config.xml).
   
   --word_size, -w SIZE
       BLASTN word size.
   


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

Once exemplars have been defined you may also wish to set the fast_scan="yes"
option in the config.xml file. This enables their use for scanning within the
web curators' interface. 

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
    
 --variation DISSIMILARITY
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

The scannew.pl script should be installed in /usr/local/bin. It is run as 
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
   --alignment, -A INT
       Percentage alignment (default: 100).
   
   --allow_frameshift
       Allow sequences to contain a frameshift so that the length is not a 
       multiple of 3, or an internal stop codon. To be used with 
       --coding_sequences option to allow automated curation of pseudogenes.
       New alleles assigned will be flagged either 'frameshift' or 'internal stop
       codon' if appropriate.  Essentially, combining these two options only 
       checks that the sequence starts with a start codon and ends with a stop
       codon.  
   
   --allow_subsequences
       Allow definition of sub- or super-sequences. By default these will not
       be assigned.  
      
   --already_tagged, -T
       Scan even when sequence tagged (no designation).    
       
   --assembly_checks
       Only run against isolates that have passed all assembly checks.
       
   --assign, -a
       Assign new alleles in definitions database.
   
   --coding_sequences, -c
       Only return complete coding sequences.
       
   --curator CURATOR ID
       Curator id to use for updates. By default -1 is used - there should be an
       autodefiner account set with this id number.
   
   --database, -d NAME
       Database configuration name.
       
   --exclude_isolates, -I LIST
       Comma-separated list of isolate ids to ignore.
       
   --exclude_loci, -L LIST
       Comma-separated list of loci to exclude.
       
   --exclude_projects, -P LIST
       Comma-separated list of projects whose isolates will be excluded.
       
   --exemplar, -e
       Only use alleles with the 'exemplar' flag set in BLAST searches to identify
       locus within genome. Specific allele is then identified using a database 
       lookup. This may be quicker than using all alleles for the BLAST search, 
       but will be at the expense of sensitivity. If no exemplar alleles are set 
       for a locus then all alleles will be used. Sets default word size to 15.
   
   --fast, -f
       Perform single BLAST query against all selected loci together. This will
       take longer to return any results but the overall scan should finish 
       quicker. This method will also use more memory - this can be used with
       --exemplar to mitigate against this.
   
   --help, -h
       This help page.
       
   --identity, -B INT
       Percentage identity (default: 99).
      
   --isolate_list_file FILE  
       File containing list of isolate ids (ignored if -i or -p used).
       
   --isolates, -i LIST
       Comma-separated list of isolate ids to scan (ignored if -p used).
              
   --loci, -l LIST
       Comma-separated list of loci to scan (ignored if -s used).
       
   --locus_regex, -R REGEX
       Regex for locus names.
       
   --max, -y ID
       Maximum isolate id.
       
   --min, -x ID
       Minimum isolate id.
   
   --min_size, -m SIZE
       Minimum size of seqbin (bp) - limit search to isolates with at least this
       much sequence.
              
   --new_only, -n
       New (previously untagged) isolates only.
       
   --new_max_alleles ALLELES
       Set the maximum number of alleles that can be designated or sequences
       tagged before an isolate is not considered new when using the --new_only
       option.
       
   --no_private
       Do not include private isolate records in scan.
   
   --order, -o
       Order so that isolates last tagged the longest time ago get scanned first.
              
   --projects, -p LIST
       Comma-separated list of project isolates to scan.
      
   --quiet, -q
       Only error messages displayed.
                 
   --reuse_blast
       Reuse the BLAST database for every isolate (when running --fast option). 
       All loci will be scanned rather than just those missing from an isolate. 
       Consequently, this may be slower if isolates have already been scanned, 
       and for the first isolate scanned by a thread. On larger schemes, such as 
       wgMLST, or when isolates have not been previously scanned, setting up the
       BLAST database can take a significant amount of time, so this may be 
       quicker.
   
   --schemes, -s LIST
       Comma-separated list of scheme loci to scan.
       
   --seqbin_reldate DAYS
       Filter to only include isolates for which the sequence bin was last
       modified within the specified number of days (set 1 for today).
   
   --time, -t MINS
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
       
   --view, -v VIEW
       Isolate database view (overrides value set in config.xml).
   
   --word_size, -w SIZE
       BLASTN word size.
    
.. _assembly_stats:

.. index::
   single: assembly stats

**************************
Calculating assembly stats
**************************
Basic assembly statistics are calculated automatically by the database engine
as contigs are added to the sequence bin. These include the number of contigs,
total length and the N50 value. Some calculations, such as %GC, number of Ns,
and the number of gaps however, require offline analysis since these involve
inspecting the nucleotide content of each contig. These can be calculated by 
running the update_assembly_stats.pl script. You can choose to run this against
all databases on the system or against a specific database. 

Only one copy of the script can run at a time, but it will stop gracefully if 
it detects another copy running, so it is recommended that the script is run 
regularly using a CRON job and the --quiet option. This ensures that records
are updated shortly after they have been uploaded.

Once calculated, all assembly statistics can then be 
:ref:`used in isolate queries<query_by_seqbin>`. 

A full list of options can be found by typing: ::

 update_assembly_stats.pl --help
 
 NAME
     update_assembly_stats.pl - Perform/update calculation of 
     assembly GC, N and gap stats.

 SYNOPSIS
     update_assembly_stats.pl [options]

 OPTIONS

 --database DATABASE CONFIG
     Database configuration name. If not included then all isolate databases
     defined on the system will be checked.
    
 --exclude CONFIG NAMES 
     Comma-separated list of config names to exclude.
    
 --help
     This help page.
      
 --quiet
     Only show errors.
    
 --refresh_days DAYS
     Refresh records last analysed longer that the number of days set. By 
     default, only records that have not been analysed will be checked. 
     
.. _rmlst_analysis:

.. index::
   pair: rMLST;storing analysis results

******************************************
Predicting species based on rMLST analysis
******************************************
The :ref:`rMLST plugin<rmlst>` predicts species based on matches to rMLST
alleles exclusively found in a particular species. It uses the PubMLST API
to query either a genome sequence or rMLST allele designations to identify
the species. When the analysis is run using the plugin, the results are also
stored with the isolate record and can then be displayed within the isolate
information page. This analysis can also be run offline using the 
update_rmlst_species.pl script.

Only one copy of the script can run at a time, but it will stop gracefully if 
it detects another copy running, so it is recommended that the script is run 
regularly using a CRON job and the --quiet option. This ensures that records
are updated shortly after they have been uploaded.

A full list of options can be found by typing: ::

 update_rmlst_species.pl --help
 
 NAME
     update_rmlst_species.pl - Perform/update species id check

 SYNOPSIS
     update_rmlst_species.pl [options]

 OPTIONS

 --database DATABASE CONFIG
     Database configuration name. If not included then all isolate databases
     defined on the system will be checked.
    
 --exclude CONFIG NAMES 
     Comma-separated list of config names to exclude.
    
 --help
     This help page.
    
 --last_run_days DAYS
     Only run for a particular isolate when the analysis was last performed
     at least the specified number of days ago.
    
 --quiet
     Only show errors.
    
 --refresh_days DAYS
     Refresh records last analysed longer that the number of days set. By 
     default, only records that have not been analysed will be checked.  

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
     
.. _gp_town_lookups:

.. index::
   pair: geographic point lookup values;populating

*****************************************
Populating geographic point lookup values
*****************************************
If a field has the geographic_point_lookup attribute set to 'yes' in the
:ref:`config.xml file<isolate_xml_field>`, field values can be mapped to GPS 
coordinates to facilitate mapping.

These lookup values can be populated using the gp_town_lookups.pl script found
in the scripts/maintenance directory. This script uses the Geonames dataset
that contains GPS coordinates for towns and cities with populations of at least
1000 people. The dataset is included in the datasets/Geonames directory.

A full list of options can be found by typing: ::

 gp_town_lookups.pl --help   
 
 NAME
     geography_point_lookups.pl - Populate geography_point_lookup table 
     to set city/town GPS coordinates for mapping.
 
 SYNOPSIS
     geography_point_lookups.pl --database NAME --field FIELD --geodataset DIR
    
     Run this to populate any unassigned values in the geography_point_lookup
     table.

 OPTIONS

 --database NAME
     Database configuration name.
    
 --feature_code CODE
     Geonames feature code. See http://www.geonames.org/export/codes.html.
     Default is 'P' (towns/cities).
    
 --field FIELD
     Name of field. This should have the geography_point_lookup attribute set to
     'yes' in config.xml.
    
 --geodataset DIR
     Directory containing the Geonames dataset.
    
 --help
     This help page.
    
 --min_population POPULATION
     Set the minimum population for town to assign. Note that all entries in the
     Geonames database has population, so setting this attribute may result in 
     some values not being assigned, but can ensure that only high-confidence 
     values are used.
    
 --quiet
     Only show error messages.
    
 --tmp_dir DIR
     Location for temporary files. Defaults to /var/tmp/.
