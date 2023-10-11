- ## Ticket details
	- [ticket](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/7047)
## Notes
	- on the VertisReactSelect component the `isMulti={false}` was sent as props,
		- the VertisReactSelect component behavior is different in case of isMulti is `true` or `false`
		- the code was not updated to
	- the field name is "Related accounts" that suggest multi selection possibility
	- we added the `isMulti={true}` back so the issue disappeared
## Review details
	- [pull request](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/459)
## Activity Summary
	- [[2023-10-11]] (30m)
		- reproduced
		- talked with #Adam.Szucs who was helping me debug and solve the issue
- tags:: #vertis #ticket