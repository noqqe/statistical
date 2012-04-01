#!/bin/bash
# statistical: gernerate easy statistical informations in bash
# Copyright: (C) 2011 Florian Baumann <flo@noqqe.de>
# License: GPL-3 <http://www.gnu.org/licenses/gpl-3.0.txt>
# Date: Tuesday 2011-04-12

### Locales 
SUM="$*"        # see all key value pairs
OUTPUTCHAR='#'  # configure this to your favorite ascii char 
BORDERCHAR='|'  # configure this to your favorite ascii char 
BIGKEY=0        # usually you dont have to touch this 

# Read from stdin hack
if [ -z "$*" ]; then
    SUM=$(cat /dev/stdin)
fi
    
### Scaling and environment analysis for optimal output on 
# the most terminals 
for data in $SUM; do

    # Getting informations from parameters
    KEY=${data%%:*}
    VALUE=${data##*:}

    # Fishing errors from wrong usage
    if [[ ! $VALUE =~ ^[[:digit:]]+$ ]]; then
        echo "ERROR: Do not use characters as value! Key:$KEY Value:$VALUE"
        exit 1
    fi

    # Bash couldn't handle values with more than 19 numbers
    # Values longer than 19 will be transformed into strings.
    # String could not be graphed :) 
    if [[ ${#VALUE} -gt 19 ]]; then 
        echo "Error: Bash couldn't handle values with more than 19 numbers. Sorry."
        exit 1
    fi

    # Doing the right formatting for a global 
    # tabulator spaces work
    if [ ${#KEY} -gt 23 ]; then 
        BIGKEY=3
    elif [ ${#KEY} -gt 15 ]; then 
        BIGKEY=2
    elif [ ${#KEY} -gt 7 ]; then 
        BIGKEY=1
    fi

    # Fishing the biggest value 
    (( VALUE > MAXVALUE )) && MAXVALUE=$VALUE

done

# Creating the right factor to fit the bars up to your terminal
FACTORCOUNT=0
FACTOR=1
while [ ${FACTORCOUNT} -lt $(( ${#MAXVALUE} - 2 )) ]; do
    FACTOR="${FACTOR}0"
    ((FACTORCOUNT++))
done

# Start graphing
for data in $SUM; do

    KEY=${data%%:*}
    VALUE=${data##*:}
    REAL_VALUE="$VALUE"
    COUNTER="0"
    
    # Do value scaling action for terminal
    VALUE=$(($VALUE / $FACTOR))
    
    # Do key scaling action for terminal
    if [ ${#KEY} -ge 23 ]; then 
        KEY=${KEY:0:22}
    fi

    # Formatting the keys for your graph
    if [ $BIGKEY -eq 3 -a ${#KEY} -lt 8 ]; then
        echo -n -e "${KEY}\t\t\t\t"
    elif [ $BIGKEY -eq 3 -a ${#KEY} -lt 15 ]; then
        echo -n -e "${KEY}\t\t\t"
    elif [ $BIGKEY -eq 3 -a ${#KEY} -lt 23 ]; then
        echo -n -e "${KEY}\t\t"
    elif [ $BIGKEY -eq 2 -a ${#KEY} -lt 8 ]; then
        echo -n -e "${KEY}\t\t\t"
    elif [ $BIGKEY -eq 2 -a ${#KEY} -lt 15 ]; then
        echo -n -e "${KEY}\t\t"
    elif [ $BIGKEY -eq 1 -a ${#KEY} -lt 8 ]; then
        echo -n -e "${KEY}\t\t"
    else
        echo -n -e "${KEY}\t"
    fi

    # Putting the choosen char for border
    echo -n "$BORDERCHAR"

    # Putting a output char for each (scaled) value 
    # If the last char was written, write the real value
    while [ $COUNTER -le $VALUE ]; do
        
        ((COUNTER++))
        
        if [ $COUNTER -gt $VALUE ]; then
            echo -n " ($REAL_VALUE)" ; echo 
        else 
            echo -n "$OUTPUTCHAR"
        fi

    done
done
