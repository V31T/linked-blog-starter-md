
## Notes

### Why use Awk?
- `awk` is a text processing tool for extracting and manipulating data
- `AWK` is very fast to run on shell
- get from slides
- Awk evolved from `sed` and `grep`
	- `sed` and `grep` blank
- Allows us to:
	- View a text file as textual dtabase made up of records (lines) and fields (columns)
	- use vars to manipulate thisndatabase
	- use arithmetic and string operations
	- use programming constructs such as loops and conditionals
	- blank
- How to use:
	- `awk 'patter {action}' filename`
	- C


A6 QUESTIONS:
1. What are all the airlines?
	"Alaska"
	"American"
	"Delta"
	"Jet Blue"
	"Southwest"
	"United"
		`awk -F, '{print $4'} airline_stats.csv | sort |  uniq`
2. Which airlines have: 
	a.  Has a carrier delay greater than 10 and print airline names (alphabetically. Hint* pipe input into sort)
		"Alaska"
		"American"
		"Delta"
		"Jet Blue"
		"Southwest"
		"United"
			`awk -F, '$1 > 10 {print $4'} airline_stats.csv | sort`
	b. Has a carrier delay greater than a certain threshold of 15? Use -v to pass in a value that is set to 'Threshold = 15'
		"Alaska"
		"American"
		"Delta"
		"Jet Blue"
		"Southwest"
		"United"
```bash
$ Threshold=15
$ awk -F, -v th=$Threshold '$1 > th {print $4}' airline_stats.csv | wc
```