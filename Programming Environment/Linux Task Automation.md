# Linux task automation

- Need a bash script and crontab

## Write a bash script

### shebang

``` bash
#!/bin/bash
```

- put this line in the beginning

### when the program requires user input

```bash
gmx energy -f nvt.edr -o temperature.xvg << EOF
16
0
EOF
```

- put inputs between EOFs

### Example

``` bash
#!/bin/bash

conda activate bioinformatics
source ~/assignment2/gmx_env.sh

# Run GROMACS pre-processing
gmx grompp -f nvt.mdp -c em.gro -r em.gro -p topol.top -o nvt.tpr

# Run GROMACS molecular dynamics
gmx mdrun -nt 1 -deffnm nvt -v 

# Run GROMACS energy command with input provided via Here Document
gmx energy -f nvt.edr -o temperature.xvg <<EOF
16
0
EOF
```

### Make executable (must run)

``` bash
chmod +x run_gmx.sh
```

## Use crontab

- Open crontab

``` bash
crontab -e
```

- Inside the window, write:

``` text
0 2 * * * /path/to/run_gmx.sh > /path/to/logfile.log 2>&1
```

- The `0 2` sets the task to start at 2:00 AM
- `2>$1` writes standard output and error messages to the log
- View log with: 

``` bash
tail -f /path/to/logfile.log
```

### check pending cron jobs

``` bash
crontab -l
```

and compare with 

``` bash
date
```

## Keep process running in background

- run immediately
- no scheduling with crontab
- use screen

### Start screen session

``` bash
screen -S <name>
```

### Run bash script in session

``` bash
./run_gmx.sh > output.log 2>&1 &
```

- The log file records standard output and error messages
- the `&` at the end puts the process in the background

### Go back to original screen

`Ctrl`+`A`+`D`

### Resume screen

``` bash
screen -r
```

### Check available screens

``` bash
screen -ls
```

### Close screen


`Ctrl` + `A`
`k`
`y`

