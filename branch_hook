#!/bin/bash
# Reject branch pushes that contain commits under those branches that have names starting with release

first_commit='0000000000000000000000000000000000000000'

while read -r oldrev newrev refname; do

    [ "$newrev" = "$first_commit" ] && continue


    [ "$oldrev" = "$first_commit" ] && range="$newrev" || range="$oldrev..$newrev"

    for commit in $(git rev-list "$range" --not --all); do
        if [[ "${refname#refs/heads/}" == release* ]]; then
    
            echo "ERROR: Your push was rejected because the commit"
            echo "ERROR: $commit in ${refname#refs/heads/}"
            echo "ERROR: is not allowed as ${refname#refs/heads/} is not supported branch name"
            echo "ERROR: Please fix your branch name or contact your repository admin."
            exit 1
        fi
    done

done
