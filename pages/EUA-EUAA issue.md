- ## Ticket details
	- [ticket](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793)
## Notes
	- Discussion about the EUA/EUAA topic
		- [part 1](https://vertiszrt-my.sharepoint.com/personal/balazs_szalma_vertis_com/_layouts/15/stream.aspx?id=%2Fpersonal%2Fbalazs_szalma_vertis_com%2FDocuments%2FRecordings%2FEUA_EUAA-20230518_102035-Meeting Recording%2Emp4&ga=1)
		- [part 2](https://vertiszrt-my.sharepoint.com/personal/balazs_szalma_vertis_com/_layouts/15/stream.aspx?id=%2Fpersonal%2Fbalazs_szalma_vertis_com%2FDocuments%2FRecordings%2FEUA_EUAA _2-20230525_100847-Meeting Recording%2Emp4&ga=1)
	- Presentation
		- [[EUA EUAA presentation]]
		- Account with strict EUA/EUAA contract set
			- Contract number: 00008637
			- Account code: 011448
		- Set "Strict EUA or EUAA" checkbox on ETS Contract
		- ETS Contract Detail view
		- ETS Offer
			- When EUA / EUAA product was choosen a checkbox appears next to the product
				- the checkbox value is the same as the value on the contract but it can be modified
		- ETS Offer List
## Review details
	- [pull request](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319)
## Activity Summary
	- [[2023-07-31]]
		- [EUA/EUAA issue](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793)'s [remaining](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793#note_13405) UI updates
	- [[2023-08-01]]
		- [EUA/EUAA issue](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793)'s [remaining](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793#note_13405) UI updates
			- Active Offers page have a separate section for strict products was challenging
				- #Adam.Szucs helped a lot
		- formatting tables
		- displaying help text for strict product checkboxes
		- rename "Strict Product" to "Strict EUA/EUAA"
		- Don't show counterparty balance if it's 0
		- set EUA's price ticker for EUAA
	- [[2023-08-02]]
		- [EUA/EUAA issue](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793)'s [remaining](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6793#note_13405) UI updates
	- [[2023-08-03]]
		- #Zoltan.Egyed checked my pull request and he left many comments
			- I fixed most of them
			- Remaining CR comments to doublecheck and/or fix:
				- [Using `quantity` instead of `unsettled_quantity`](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14508)
				- [Passing commodity id list instead of commodity name list](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14512)
				- [FIFO should work without the commodities `EUA` or `EUAA`](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14587)
	- [[2023-08-04]]
		- [remaining PR comments fixed](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319) (4h)
			- fixed [Passing commodity id list instead of commodity name list](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14512)
			- fixed [Using `quantity` instead of `unsettled_quantity`](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14508)
			- fixed [FIFO should work without the commodities `EUA` or `EUAA`](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/319#note_14587)
	- [[2023-08-07]]
		- fix table coloring (5m)
		- fix table size (25m)
		  :LOGBOOK:
		  CLOCK: [2023-08-07 Mon 11:01:51]--[2023-08-07 Mon 11:01:56] =>  00:00:05
		  CLOCK: [2023-08-07 Mon 11:02:28]--[2023-08-07 Mon 11:02:34] =>  00:00:06
		  :END:
	- [[2023-08-08]]
		- prepare presentation
- tags:: #vertis #ticket