- ## Ticket details
	- [ticket](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6205)
## Notes
	- AccountAML and ContactAML rules are the same
		- Identification Type: (rename mode):
			- simplified -> e-mail
		- Risk Level -> Table will be created from the possible choices in BO.
			- Low
				- mode: simplified
			- Normal
			- High
		- Risk Category
		- Summary:
			- From Risk Level, the Identification Type (mode) choices will be obvious
			- Set the Risk Category, define possible choices
				- There will be an `undefined` choice which we'll apply for all the current AMLs
					- BO will set the AML with Risk Category undefined
					- The undefined category cannot be set manually
## Review details
	- [pull request](link.to.pull.request)
## Activity Summary
	- [[2023-08-07]]
		- Reading the ticket's description (30m)
	- [[2023-08-08]]
		- Meeting @11:00 with #Eszter.Toth and #Balazs.Szalma about the topic
	-
- tags:: #vertis #ticket