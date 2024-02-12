- [how to set browser tab title and logo](https://stackoverflow.com/questions/51688463/shiny-page-title-and-image)
	- also see isotopeApp code for how to set for navbar pages

## Shinyapps.io

- [Dashboard](https://www.shinyapps.io/admin/#/dashboard)
- [usage tracking tutorial](https://shiny.posit.co/r/articles/improve/usage-metrics/)
- Set auto-sleep to 5 minutes in dashboard to reduce wasting usage!
- deploy:
```r
rsconnect::setAccountInfo(name='jumpingbeaver',
			  token='EB2F582554225807257EAEBB2F9283CC',
			  secret='<SECRET>')
rsconnect::deployApp('./counter/')
```
see secret at account>tokens
## Bug reports 😭

### [shinyDirChoose does not work on shinyapps.io](https://github.com/thomasp85/shinyFiles/issues/190)

