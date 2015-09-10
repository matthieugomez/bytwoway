# Stata-bytwoway

`bytwoway` is a convenience command to plot graphs by group in Stata.



## Aesthetics option

Make an aesthetic varies by group using the option aesthetics. Available aesthetics are mcolor, lcolor, lpattern and msymbol 

```
sysuse nlsw88.dta, clear
collapse (mean) wage, by(grade race)
bytwoway (line wage grade), by(race) aes(color lpattern)
```
![](img/aeslpattern.jpg)


```
bytwoway (scatter wage grade, connect(l)), by(race) aes(color msymbol)
```
![](img/within.jpg)



Specify a particular list to cycle through by appending the aesthetic name with an s 
```
bytwoway line wage grade, by(race) aes(color) colors("248 118 109" "0 186 56"  "97 156 255")
```
![](img/aescolors.jpg)
Use any color palette from the package [colorscheme](https://github.com/matthieugomez/stata-colorscheme) using the option `palette`

```
bytwoway line wage grade, by(smsa race) palette(GnBu)
```
![](img/palette.jpg)




## Multiple groups

Define groups on the fly with multiple variables

```
sysuse nlsw88.dta, clear
collapse (mean) wage, by(grade smsa race)
bytwoway line wage grade, by(smsa race)
```
![](img/groups.jpg)




## Script

`bytwoway` returns the macro `r(cmd)` that generates the final graph:

```
macros:
   	r(cmd) : twoway (line wage grade in 1/16, mcolor(`"navy"') lcolor(`"navy"') ///
			lpattern(`"solid"') msymbol(`"circle"') legend(label(1 white))) (line wage grade in ///
			17/32, mcolor(`"maroon"') lcolor(`"maroon"') lpattern(`"solid"') msymbol(`"circle"') /// 
			legend(label(2 black))) (line wage grade in 33/43, mcolor(`"forest_green"') ///
			lcolor(`"forest_green"') lpattern(`"solid"') msymbol(`"circle"') ///
			legend(label(3 other))),  legend(subtitle(`"race"'))  
```

# Installation

```
net install bytwoway, from(https://github.com/matthieugomez/stata-bytwoway/raw/master)
```

If you have a version of Stata < 13, you need to install it manually

1. Click the "Download ZIP" button in the right column to download a zipfile. 
2. Extract it into a folder (e.g. ~/SOMEFOLDER)
3. Run

	```
	cap ado uninstall bytwoway
	net install bytwoway, from("~/SOMEFOLDER")
	```
