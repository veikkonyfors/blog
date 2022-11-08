---
layout: default
title:  "Quoting lines for a list"
description: "Quote abunch of lines for forming a list"
tag: Unix
---

Often one needs to take a bunch of lines from web page or somewhere to form a list structure out of them. One needs to quote the lines and append comma in the end.

Handy way of doing it below:

	pappa@pappa-ThinkPad-X270:~$ cat <<EAF | sed -e's/^/"/' -e's/$/",/'
	> eyr:1972 cid:100
	> hcl:#18171d ecl:amb hgt:170 pid:186cm iyr:2018 byr:1926
	> 
	> iyr:2019
	> hcl:#602927 eyr:1967 hgt:170cm
	> ecl:grn pid:012533040 byr:1946
	> 
	> hcl:dab227 iyr:2012
	> ecl:brn hgt:182cm pid:021572410 eyr:2020 byr:1992 cid:277
	> 
	> hgt:59cm ecl:zzz
	> eyr:2038 hcl:74454a iyr:2023
	> pid:3556412378 byr:2007
	> EAF
	"eyr:1972 cid:100",
	"hcl:#18171d ecl:amb hgt:170 pid:186cm iyr:2018 byr:1926",
	"",
	"iyr:2019",
	"hcl:#602927 eyr:1967 hgt:170cm",
	"ecl:grn pid:012533040 byr:1946",
	"",
	"hcl:dab227 iyr:2012",
	"ecl:brn hgt:182cm pid:021572410 eyr:2020 byr:1992 cid:277",
	"",
	"hgt:59cm ecl:zzz",
	"eyr:2038 hcl:74454a iyr:2023",
	"pid:3556412378 byr:2007",
	pappa@pappa-ThinkPad-X270:~$ 

In vi, one could use commands ':1,$s/^/"/' and ':1,$s/$/",/'

List below (in Kotlin)

	val listOfCredentialLines:List<String> = listOf(
		"eyr:1972 cid:100",
		"hcl:#18171d ecl:amb hgt:170 pid:186cm iyr:2018 byr:1926",
		"",
		"iyr:2019",
		"hcl:#602927 eyr:1967 hgt:170cm",
		"ecl:grn pid:012533040 byr:1946",
		"",
		"hcl:dab227 iyr:2012",
		"ecl:brn hgt:182cm pid:021572410 eyr:2020 byr:1992 cid:277",
		"",
		"hgt:59cm ecl:zzz",
		"eyr:2038 hcl:74454a iyr:2023",
		"pid:3556412378 byr:2007"
		)