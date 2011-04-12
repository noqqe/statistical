# statistical

statistical is a tiny easy-to-use bash script for visualizing simple data in your terminal. 

## Usage 

statistical is following a simple key:value scheme like in json or similar. Just
add key:value pairs as parameters and watch the generic statistical graph

It probably looks like github is ignoring my tabs and tabulators in formatting.
Be sure that formatting in your terminal is working correctly!

    # Closed RT Tickets by RequestTracker sorted by user (for example)
    $ statistical john:433 alice:49 linus:12 bob:231 
    john    |###########################################
    alice   |####
    linus   |#
    bob     |#######################

Maybe a some more complex example. There is a bit bash magic :) statistical can read from stdin as well. So you can just pipe some formated informations into it like:

    $ cd ~/Projects/bash-it
    $ for a in $(git shortlog -sn --all | cut -f2 | cut -f1 -d' '); do echo -n "$a:" ; git log $LOGOPTS --all --numstat --format="%n" --author=$a | cut -f3 | sort -iu | wc -l; done  | statistical
    Mark          |##################
    Robert        |#########################################################################
    Florian       |##############
    Jesus         |######
    John          |##############
    Rich          |########
    Piotr         |###
    Travis        |####
    Fedyashev     |##
    zerobearing2  |####
    Andy          |###
    Daniel        |####
    Jeff          |##
    Karl          |##
    Robert        |#########################################################################
    Sirupsen      |##

