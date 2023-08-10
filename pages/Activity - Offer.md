- ## Ticket details
	- [ticket](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/6764)
## Notes
	- Review details
		- Investigate problem: `SerializerMethodField.input.validation`
			- [PR comment](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/312#note_13229) There was an interesting issue while Adam was resolving my PR comment. He created a method for validation:
			- ```python
			  def validate_ets_offers(self, value):
			  	...
			      
			  ```
			- the validation does not run, the ets_offer is a `serializers.SerializerMethodField()`
## Review details
	- [pull request](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/312)
## Activity Summary
	- [[2023-07-25]]
		- review the code
	- [[2023-08-10]] (3)
		- fixing filtering on the frontend
		- fixing modal size on the frontend
- tags:: #vertis #ticket #Adam.Szucs