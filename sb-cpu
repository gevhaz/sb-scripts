#!/bin/sh

load() {
    read -r _ a b c previdle rest </proc/stat
    prevtotal=$((a + b + c + previdle))
    sleep 0.5
    read -r _ a b c idle rest </proc/stat
    total=$((a + b + c + idle))

    load=$((100 * ((total - prevtotal) - (idle - previdle)) / (total - prevtotal)))
    echo $load | numfmt --format "%2.0f"
}

temp() {
    temp=$(sensors | awk '/Core 0/ { print $3 }' | sed "s/+//;s/\.[0-9]//;s/°C//")
    echo "$temp"
}

mem() {
    echo " $(free -h --giga | awk '/^Mem:/ { print $3 }')"
}

load="$(load)"
temp="$(temp)"
mem="$(mem)"

# echo "CPU: $load $temp"
# echo "$mem  $load  $temp"
echo " ${load}%  ${temp}°C"
