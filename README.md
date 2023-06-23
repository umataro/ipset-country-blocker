# ipset-country-blocker

BLOCK traffic to/from/through your server from/to entire countries easily with this script. All you need is iptables, ipset, curl and bash.

## Description
This script allows you to easily block traffic from/to countries via ipset and iptables. It does this by:

* downloading country prefixes
* creating an ip set for each country specified in `country_codes.txt` file
* creating a COUNTRYBLOCK chain that drops packets from prefixes defined in those ipsets
* inserting a jump to this COUNTRYBLOCK chain into INPUT, FORWARD and OUTPUT chains

TODO:
~It can be controlled via a systemd unit file - supporting `start`, `stop`, `reload` functionality, where reload will refresh prefixes. Or it can be used standalone, where it also supports `pause`, `unpause`. This keeps sets in COUNTRYBLOCK, but remove/reinstate the jump to this chain from built-in chains.~~

## Installation
If you aren't installing from a package, make sure you have `ipset`, `iptables`, `curl` and `bash` installed. There are no other dependencies. Place the script into `/usr/local/bin/` and its `country_codes.txt` file alongside it.

## Configuration
Visit https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements to get the 2 character ISO country codes for the countries you want to block. Put those into country_codes.txt - 1 country per line. **No empty lines**, **no comments**, **no upper case characters** are allowed. Do not press Enter after the last entry in the file (which creates a new empty line). For example, to block China, Russia and Ukraine, the file would contain the following 3 lines:
```
cn
ru
ua
```

## Usage

### In standalone mode
* `./ipset-country-blocker -a` - (add) - sets up country blocking
* `./ipset-country-blocker -d` - (delete) - stops country blocking (removes all chains, rules and sets related to this)
* `./ipset-country-blocker -r` - (refresh) - refreshes lists of prefixes that ipset uses for country blocking (without stopping/starting)
* `./ipset-country-blocker -p` - (pause) - temporarily pauses country blocking (doesn't do full teardown of sets, rules, chain - only removes jumps to COUNTRYBLOCK chain)
* `./ipset-country-blocker -u` - (unpause) - resumes paused country blocking (restores jumps to COUNTRYBLOCK chain)
* `./ipset-country-blocker -h` - (help) - displays a helpful message with expected syntax

### ~~In systemd mode~~ TODO
* ~~`systemctl start ipset-country-blocker` - sets up country blocking~~
* ~~`systemctl stop ipset-country-blocker` - stops country blocking (removes all chains, rules and sets related to this)~~
* ~~`systemctl reload ipset-country-blocker` - refreshes lists of prefixes that ipset uses for country blocking (without stopping/starting)~~

## Support
Read the code. It is actually really easy to understand.

## Contributing
If you have functionality to add, it is very unlikely it'll be added as this is a small single purpose project. Just fork the project under the terms of GPLv3 or later license and make it your own.

## Authors and acknowledgment
Written by umataro@live.com in 2022

## License
GPLv3 or later

## Project status
Work in progress

## Appendix 1 - country codes and names

As of 2022-10-10, these country codes exist


| country code | country name |
| ------ | ------ |
|	ad	|	Andorra	|
|	ae	|	United Arab Emirates	|
|	af	|	Afghanistan	|
|	ag	|	Antigua and Barbuda	|
|	ai	|	Anguilla	|
|	al	|	Albania	|
|	am	|	Armenia	|
|	ao	|	Angola	|
|	aq	|	Antarctica	|
|	ar	|	Argentina	|
|	as	|	American Samoa	|
|	at	|	Austria	|
|	au	|	Australia	|
|	aw	|	Aruba	|
|	ax	|	Åland Islands	|
|	az	|	Azerbaijan	|
|	ba	|	Bosnia and Herzegovina	|
|	bb	|	Barbados	|
|	bd	|	Bangladesh	|
|	be	|	Belgium	|
|	bf	|	Burkina Faso	|
|	bg	|	Bulgaria	|
|	bh	|	Bahrain	|
|	bi	|	Burundi	|
|	bj	|	Benin	|
|	bl	|	Saint Barthélemy	|
|	bm	|	Bermuda	|
|	bn	|	Brunei Darussalam	|
|	bo	|	Bolivia (Plurinational State of)	|
|	bq	|	Bonaire, Sint Eustatius and Saba	|
|	br	|	Brazil	|
|	bs	|	Bahamas	|
|	bt	|	Bhutan	|
|	bv	|	Bouvet Island	|
|	bw	|	Botswana	|
|	by	|	Belarus	|
|	bz	|	Belize	|
|	ca	|	Canada	|
|	cc	|	Cocos (Keeling) Islands	|
|	cd	|	Congo, Democratic Republic of the	|
|	cf	|	Central African Republic	|
|	cg	|	Congo	|
|	ch	|	Switzerland	|
|	ci	|	Côte d'Ivoire	|
|	ck	|	Cook Islands	|
|	cl	|	Chile	|
|	cm	|	Cameroon	|
|	cn	|	China	|
|	co	|	Colombia	|
|	cr	|	Costa Rica	|
|	cu	|	Cuba	|
|	cv	|	Cabo Verde	|
|	cw	|	Curaçao	|
|	cx	|	Christmas Island	|
|	cy	|	Cyprus	|
|	cz	|	Czechia	|
|	de	|	Germany	|
|	dj	|	Djibouti	|
|	dk	|	Denmark	|
|	dm	|	Dominica	|
|	do	|	Dominican Republic	|
|	dz	|	Algeria	|
|	ec	|	Ecuador	|
|	ee	|	Estonia	|
|	eg	|	Egypt	|
|	eh	|	Western Sahara	|
|	er	|	Eritrea	|
|	es	|	Spain	|
|	et	|	Ethiopia	|
|	fi	|	Finland	|
|	fj	|	Fiji	|
|	fk	|	Falkland Islands (Malvinas)	|
|	fm	|	Micronesia (Federated States of)	|
|	fo	|	Faroe Islands	|
|	fr	|	France	|
|	ga	|	Gabon	|
|	gb	|	United Kingdom of Great Britain and Northern Ireland	|
|	gd	|	Grenada	|
|	ge	|	Georgia	|
|	gf	|	French Guiana	|
|	gg	|	Guernsey	|
|	gh	|	Ghana	|
|	gi	|	Gibraltar	|
|	gl	|	Greenland	|
|	gm	|	Gambia	|
|	gn	|	Guinea	|
|	gp	|	Guadeloupe	|
|	gq	|	Equatorial Guinea	|
|	gr	|	Greece	|
|	gs	|	South Georgia and the South Sandwich Islands	|
|	gt	|	Guatemala	|
|	gu	|	Guam	|
|	gw	|	Guinea-Bissau	|
|	gy	|	Guyana	|
|	hk	|	Hong Kong	|
|	hm	|	Heard Island and McDonald Islands	|
|	hn	|	Honduras	|
|	hr	|	Croatia	|
|	ht	|	Haiti	|
|	hu	|	Hungary	|
|	id	|	Indonesia	|
|	ie	|	Ireland	|
|	il	|	Israel	|
|	im	|	Isle of Man	|
|	in	|	India	|
|	io	|	British Indian Ocean Territory	|
|	iq	|	Iraq	|
|	ir	|	Iran (Islamic Republic of)	|
|	is	|	Iceland	|
|	it	|	Italy	|
|	je	|	Jersey	|
|	jm	|	Jamaica	|
|	jo	|	Jordan	|
|	jp	|	Japan	|
|	ke	|	Kenya	|
|	kg	|	Kyrgyzstan	|
|	kh	|	Cambodia	|
|	ki	|	Kiribati	|
|	km	|	Comoros	|
|	kn	|	Saint Kitts and Nevis	|
|	kp	|	Korea (Democratic People's Republic of)	|
|	kr	|	Korea, Republic of	|
|	kw	|	Kuwait	|
|	ky	|	Cayman Islands	|
|	kz	|	Kazakhstan	|
|	la	|	Lao People's Democratic Republic	|
|	lb	|	Lebanon	|
|	lc	|	Saint Lucia	|
|	li	|	Liechtenstein	|
|	lk	|	Sri Lanka	|
|	lr	|	Liberia	|
|	ls	|	Lesotho	|
|	lt	|	Lithuania	|
|	lu	|	Luxembourg	|
|	lv	|	Latvia	|
|	ly	|	Libya	|
|	ma	|	Morocco	|
|	mc	|	Monaco	|
|	md	|	Moldova, Republic of	|
|	me	|	Montenegro	|
|	mf	|	Saint Martin (French part)	|
|	mg	|	Madagascar	|
|	mh	|	Marshall Islands	|
|	mk	|	North Macedonia	|
|	ml	|	Mali	|
|	mm	|	Myanmar	|
|	mn	|	Mongolia	|
|	mo	|	Macao	|
|	mp	|	Northern Mariana Islands	|
|	mq	|	Martinique	|
|	mr	|	Mauritania	|
|	ms	|	Montserrat	|
|	mt	|	Malta	|
|	mu	|	Mauritius	|
|	mv	|	Maldives	|
|	mw	|	Malawi	|
|	mx	|	Mexico	|
|	my	|	Malaysia	|
|	mz	|	Mozambique	|
|	na	|	Namibia	|
|	nc	|	New Caledonia	|
|	ne	|	Niger	|
|	nf	|	Norfolk Island	|
|	ng	|	Nigeria	|
|	ni	|	Nicaragua	|
|	nl	|	Netherlands	|
|	no	|	Norway	|
|	np	|	Nepal	|
|	nr	|	Nauru	|
|	nu	|	Niue	|
|	nz	|	New Zealand	|
|	om	|	Oman	|
|	pa	|	Panama	|
|	pe	|	Peru	|
|	pf	|	French Polynesia	|
|	pg	|	Papua New Guinea	|
|	ph	|	Philippines	|
|	pk	|	Pakistan	|
|	pl	|	Poland	|
|	pm	|	Saint Pierre and Miquelon	|
|	pn	|	Pitcairn	|
|	pr	|	Puerto Rico	|
|	ps	|	Palestine, State of	|
|	pt	|	Portugal	|
|	pw	|	Palau	|
|	py	|	Paraguay	|
|	qa	|	Qatar	|
|	re	|	Réunion	|
|	ro	|	Romania	|
|	rs	|	Serbia	|
|	ru	|	Russian Federation	|
|	rw	|	Rwanda	|
|	sa	|	Saudi Arabia	|
|	sb	|	Solomon Islands	|
|	sc	|	Seychelles	|
|	sd	|	Sudan	|
|	se	|	Sweden	|
|	sg	|	Singapore	|
|	sh	|	Saint Helena, Ascension and Tristan da Cunha	|
|	si	|	Slovenia	|
|	sj	|	Svalbard and Jan Mayen	|
|	sk	|	Slovakia	|
|	sl	|	Sierra Leone	|
|	sm	|	San Marino	|
|	sn	|	Senegal	|
|	so	|	Somalia	|
|	sr	|	Suriname	|
|	ss	|	South Sudan	|
|	st	|	Sao Tome and Principe	|
|	sv	|	El Salvador	|
|	sx	|	Sint Maarten (Dutch part)	|
|	sy	|	Syrian Arab Republic	|
|	sz	|	Eswatini	|
|	tc	|	Turks and Caicos Islands	|
|	td	|	Chad	|
|	tf	|	French Southern Territories	|
|	tg	|	Togo	|
|	th	|	Thailand	|
|	tj	|	Tajikistan	|
|	tk	|	Tokelau	|
|	tl	|	Timor-Leste	|
|	tm	|	Turkmenistan	|
|	tn	|	Tunisia	|
|	to	|	Tonga	|
|	tr	|	Türkiye	|
|	tt	|	Trinidad and Tobago	|
|	tv	|	Tuvalu	|
|	tw	|	Taiwan, Province of China	|
|	tz	|	Tanzania, United Republic of	|
|	ua	|	Ukraine	|
|	ug	|	Uganda	|
|	um	|	United States Minor Outlying Islands	|
|	us	|	United States of America	|
|	uy	|	Uruguay	|
|	uz	|	Uzbekistan	|
|	va	|	Holy See	|
|	vc	|	Saint Vincent and the Grenadines	|
|	ve	|	Venezuela (Bolivarian Republic of)	|
|	vg	|	Virgin Islands (British)	|
|	vi	|	Virgin Islands (U.S.)	|
|	vn	|	Viet Nam	|
|	vu	|	Vanuatu	|
|	wf	|	Wallis and Futuna	|
|	ws	|	Samoa	|
|	ye	|	Yemen	|
|	yt	|	Mayotte	|
|	za	|	South Africa	|
|	zm	|	Zambia	|
|	zw	|	Zimbabwe	|
