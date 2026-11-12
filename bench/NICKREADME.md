## NEW ADDITIONS TO BENCHMARKS ##
Added a way to customize the size of buckets, number of paths that can be ran in a bench
Bucket size = Z (default = 4, can be 2-5}
Eviction paths = P (2 or 1)

Fields: 
bucket_size: How many blocks are held in each bucket in the ORAM tree

read_paths: How many extra paths that are read which are then evicted,
if empty then it just returns the pointers normal val

ordered_evict: True if you want to do reverse lexicographic, 
False if you want random

## COMMAND LINE FLAGS ##
--bucket-size N or --z N
--paths N
--evict ordered or --evict random

## WHAT HAS NOT BEEN CHANGED ##
Dry runs will still ignore the new settings
bandwidth_table.py will assume Z = 4 and 3 paths in its model
Slower builds due to each pair being compiled for every block size and pointer type,
list fewer paies in the [match] the range checks will speed it up

Baseline:

```bash
"Baseline:"
python launch_rust_tests.py --mode crypto --pointers multiwriterary --block-sizes 64 --degrees 20 --min-power 7 --max-power 10 --trials 10

"Smaller Buckets:"
python launch_rust_tests.py --mode crypto --pointers multiwriterary --block-sizes 64 --degrees 20 --min-power 7 --max-power 10 --trials 10 --bucket-size 3

"More Eviction Paths:"
python launch_rust_tests.py --mode crypto --pointers multiwriterary --block-sizes 64 --degrees 20 --min-power 7 --max-power 10 --trials 10 --paths 3

"Random Eviction:"
python launch_rust_tests.py --mode crypto --pointers multiwriterary --block-sizes 64 --degrees 20 --min-power 7 --max-power 10 --trials 10 --evict random

"Combined table for all runs:"
python launch_rust_tests.py --report-only
```
## WHAT TO DO NEXT ##
Improve the actual rust results files so I can easily access specific runs
Start benching from this point (ER benches for fuller): C:\Users\coolm\OneDrive\Research-Nick\rust_osam_plus\bench\results\rust-logs\ER_n-65536_d-20_bs-64_trials-50-50_pt-multiwriterary_cache-true_mode-dry-run_b-6.log.partial