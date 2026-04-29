# Challenge 17 - Text Processing with sed, awk, and Pipes

[< Previous Challenge](./Challenge-16.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-18.md)

## Description

Linux excels at text processing. The ability to chain commands together with pipes and use powerful tools like sed and awk is what makes Linux administration efficient. These skills are essential for parsing logs, transforming configuration files, and automating data extraction.

## Tasks

1. Create a sample log file for exercises:

```bash
sudo cp /var/log/syslog /tmp/practice.log 2>/dev/null || sudo journalctl --no-pager -n 200 > /tmp/practice.log
```

2. Use `cut` to extract the first three fields (date/time/hostname) from each line: `cut -d' ' -f1-3 /tmp/practice.log | head -10`
3. Use `sort` and `uniq -c` to find the top 10 most frequent words in column 5 of the log: `awk '{print $5}' /tmp/practice.log | sort | uniq -c | sort -rn | head -10`
4. Use `tr` to convert the first 5 lines of the log to uppercase: `head -5 /tmp/practice.log | tr '[:lower:]' '[:upper:]'`
5. Use `sed` to replace all occurrences of your hostname with "REDACTED" in the log and save the output: `sed 's/yourhostname/REDACTED/g' /tmp/practice.log > /tmp/redacted.log`
6. Use `sed` to delete all blank lines from a file: `sed '/^$/d' /tmp/practice.log`
7. Use `awk` to print only lines longer than 80 characters: `awk 'length > 80' /tmp/practice.log | head -10`
8. Use `awk` to sum a numeric column. First create a test file:

```bash
echo -e "apples 5\nbananas 12\noranges 3\ngrapes 8" > /tmp/fruits.txt
awk '{sum += $2} END {print "Total:", sum}' /tmp/fruits.txt
```

9. Build a pipeline to find unique IP addresses in a log file (if any exist): `grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' /tmp/practice.log | sort -u`
10. Count how many .conf files exist under /etc: `find /etc -name "*.conf" 2>/dev/null | wc -l`

## Success Criteria

1. You can extract specific columns from structured text
2. You can find the most frequent items in a dataset
3. You can perform find-and-replace operations with sed
4. You can filter and aggregate data with awk
5. You can build multi-stage pipelines combining multiple tools

## Learning Resources

- [GNU sed manual](https://www.gnu.org/software/sed/manual/sed.html)
- [GNU awk manual](https://www.gnu.org/software/gawk/manual/gawk.html)
- [Linux text processing commands](https://tldp.org/LDP/abs/html/textproc.html)
- [Pipe and redirect tutorial](https://ryanstutorials.net/linuxtutorial/piping.php)

## Bridge to Kubernetes

In Kubernetes, you'll frequently pipe kubectl output through text processing tools — for example, `kubectl get pods | awk '{print $1, $3}'` to extract pod names and statuses, or `kubectl logs <pod> | grep ERROR` to filter application logs.
