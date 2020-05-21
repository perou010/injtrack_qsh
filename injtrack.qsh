if [ "$#" -lt 3 ]; then
	echo "Expecting at least 3 arguments. Exiting..."
	exit 1
fi

carrier="FEDEX"
if [ ${3:0:2} == "1Z" ]
then 
	carrier="UPS"
fi

plural="numbers are"
if [ "$#" -eq 3 ]
then plural="number is"
fi

header="<p>The following $carrier tracking $plural for Order #$1, PO $2</p>"

s=""
if [ "$carrier" == "UPS" ]
then
	sb="<li><a href=\"https://www.ups.com/mobile/track?trackingNumber="
elif [ "$carrier" == "FEDEX" ]
then
	sb="<li><a href=\"https://www.fedex.com/apps/fedextrack/?action=track&tracknumbers="
fi
sm="\">"
se="</a></li>\n"

i=1
for t in "$@"
do
	if [ $i -gt 2 ]
	then
		s="$s$sb$t$sm$t$se"
	fi
	i=$((i+1))
done

sed "/!--header--/ i $header" template.html | sed "/!--tracking_list--/ i $s" > order.html
